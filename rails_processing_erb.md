### Passing server-side data to Stimulus controllers

How Rails decides what to ERB-process:

  1. Views (app/views/**/*.erb) - Always processed. Rails sees the .erb extension and runs
  it through the ERB processor before sending to browser.
  2. Static JS (app/javascript/**/*.js) - Never processed. These files are served as-is (via
   importmap or bundler). Rails doesn't touch the contents.
  3. Inline <script> tags in .erb views - Processed, because they're inside an ERB file.

So, when you want to use something like Rails credentials inside a Stimulus controller, you can't simply interpolate the value like so:

`some_controller.js`
```js
const searchClient = algoliasearch('<%= Rails.application.credentials.algolia[:application_id] %>',
                                   '<%= Rails.application.credentials.algolia[:search_api_key] %>');
```

This is because Rails doesn't ERB-process any .js files. It worked this way when you used your `<script>` tag for the initial iteration of the search feature, because that tag was, of course, inside a .erb file.

So, how do we use Rails credentials when trying to initialize this search client in a Stimulus controller (ie, .js file)?

When working with Stimulus controllers, use `values` in your controller and `data-` attributes in your view file, specifically on the the controller element (which in this case is our `<header>` in the app layout).

So, first, here's how to define the `values` in your controller:
```js
export default class extends Controller {
  static targets = ["hits", "hitsDesktop", "searchbox", "searchboxDesktop"]
  static values = {
    appId: String,
    searchKey: String
  }

  connect() {
    const { liteClient: algoliasearch } = window['algoliasearch/lite'];
    const searchClient = algoliasearch(this.appIdValue, this.searchKeyValue);
    // ... rest of code
  }
}
```

Next, here's how to define the `data-` attributes that hold our credentials in the html:
```erb
<header class="relative"
        data-controller="algolia-search"
        data-algolia-search-app-id-value="<%= Rails.application.credentials.algolia[:application_id] %>"
        data-algolia-search-search-key-value="<%= Rails.application.credentials.algolia[:search_api_key] %>"
>
```

Naming convention notes:
- `appId` (js camelcase) corresponds directly to `data-algolia-search-app-id-value` (html kebab-case)
- to access this in the Stimulus controller, use `this.appIdValue`
