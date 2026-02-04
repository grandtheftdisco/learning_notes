## Understanding Turbo Navigation vs Normal Browser Page Loads

relevant view file:
```erb
<div class="checkout-new-page">
  <div>
    <h1 class="page-title">checkout</h1>
  </div>
  <div id="stripe-key" data-publishable-key="<%= Rails.application.credentials.dig(:stripe, :publishable_key) %>"></div>

  <div id="checkout-element"></div>

  <script src="<%= asset_path 'checkout.js' %>"></script>
</div>
```

relevant script file:
```js
document.addEventListener('DOMContentLoaded', function () {
  // this is the only way to successfully retrieve the pubkey without getting a console error that the pubkey is not a 'modern' Stripe key
  const stripeKey = document.getElementById('stripe-key').dataset.publishableKey;
  const stripe = Stripe(stripeKey);

  fetch('/checkout_sessions', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'X-CSRF-Token': document.querySelector('meta[name="csrf-token"]').getAttribute('content'),
    },
  })
  .then(response => {
    if (!response.ok) {
      // Handle HTTP errors (e.g., 404, 500)
      console.error('HTTP error:', response.status);
      return response.text().then(text => { 
        // Get the text of the error page.
        console.error('Error details:', text);
        if (response.status === 500 ) {
          console.error('Server encountered an internal error.');
          alert('An unexpected server error occurred. Please try again later.');
        } else {
          throw new Error(`HTTP error! status: ${response.status}`);
        };
      });
    }
    return response.json();
  })
  .then((data) => {
    return stripe.initEmbeddedCheckout({
      clientSecret: data.clientSecret
    });
  })
  .then((checkout) => {
    checkout.mount('#checkout-element');
  })
  .catch(error => {
    console.error('Error:', error);
  });
});
```

### regarding line 19 in script:

- `DOMContentLoaded` is a browser event that fires once: when the HTML document has finished parsing.
- "Parsing" means that the browser has read all of the HTML and built the DOM tree. It does NOT wait for images, stylesheets, etc: just the HTML structure.
- The reason it's commonly used:
  - if you put a script at the top of a page, and it tries to access your `stripe-key` as in line 21 above, that element technically doesn't exist yet, because the browser hasn't parsed that far down.
  - `DOMContentLoaded` says "wait until the whole document is parsed, THEN run this code."

```js
// Without DOMContentLoaded - might fail if script is in <head>
const el = document.getElementbyId('stripe-key') // `null` - doesn't exist yet

// With DOMContentLoaded wrapper - safe regardless of where script lives
// A callback is used to wait until the DOM has been fully parsed
document.addEventListener('DOMContentLoaded', function() {
  const el = document.getElementById('stripe-key')
})
```

### Why `DOMContentLoaded` conflicts with Rails-native Turbo in my situation above

A normal browser page load looks like this:
1. User clicks a link
2. Browser navigates to the URL
3. Browser makes a full HTTP request
4. Server returns HTML
5. Browser tears down the current page completely
6. Browser builds a brand new page from scratch (ie, builds DOM)
7. `DOMContentLoaded` fires

Turbo navigation looks like this:
1. User clicks a link
2. Turbo intercepts the click before the browser handles it
3. Turbo uses JS's Fetch API (`fetch`) to grab the new page's HTML in the background
4. The current page stays alive: nothing is torn down
5. Turbo swaps the content of the current HTML `<body>` element with that of the fetched ("new"/incoming) page.
    - The `<head>` stays untouched: stylesheets, scripts, meta tags, etc. All of this persists throughout navigation.
6. No full page rebuild, thus, `DOMContentLoaded` never fires

- In short, Steps 3 & 4 never happen in our above code examples, because `DOMContentLoaded` already fired when the app first loaded. Turbo never reloads a full page -- only changes --, so `DOMContentLoaded` won't fire again. The script runs, adds a listener for an event that will never happen, and then nothing else occurs.

### solution
- Removing the `DOMContentLoaded` wrapper is safe
- The script tag is at the bottom of the view, _after_ `#stripe-key` and `#checkout-element`. 
- So, by the time the script executes -- whether via initial page load or Turbo swap -- those elements are already in the DOM.
- The `DOMContentLoaded` wrapper's initial intent was defensive, but it's now unnecessary given the script's posiition.

### what to do if you have a script in a `<head>` tag
- use `turbo:load`

```js
// In <head> - use turbo:load instead of DOMContentLoaded
document.addEventListener('turbo:load', function() {
  const stripeKey = document.getElementById('stripe-key')?.dataset.publishableKey;
  if (!stripeKey) return;

  const stripe = Stripe(stripeKey);
  // ... rest of Stripe initialization
});
```

Two differences from `DOMContentLoaded`:
- `turbo:load` fires on initial load AND every Turbo navigation, so Stripe would initialize whenever you land on the checkout page.
- The guard clause `if (!stripeKey) return`: since this script would run on every page navigation -- not just checkout -- it needs to be able to bail out early when `#stripe-key` doesnt' exist. 
  - Without it, you'd get a null error on every other page in the app.

Of course, putting your script tag is cleaner whenver possible: no guard clause needed, no listener accumulation risk.
