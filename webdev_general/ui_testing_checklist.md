# UI Testing Checklist: By Breakpoint

Set your viewport once, run all flows, then move to the next breakpoint.

---

## Breakpoint 1: Mobile XS Portrait (375px)

### Homepage
- [ ] Hero renders, no overflow
- [ ] Images load without layout shift
- [ ] Hamburger menu visible, opens/closes
- [ ] Cart icon visible in header
- [ ] Footer stacks properly, links work

### Navigation & Header
- [ ] Logo links home
- [ ] Mobile menu opens, all links work
- [ ] Cart dropdown opens/closes
- [ ] Cart dropdown closes on outside click
- [ ] Cart badge shows correct count

### Products Index
- [ ] Product grid is single column
- [ ] Product cards render fully
- [ ] Images load, prices display
- [ ] Tap product → goes to show page

### Product Show
- [ ] Image displays correctly
- [ ] Price visible
- [ ] Description readable, no overflow
- [ ] Add to cart button visible and tappable
- [ ] Add to cart works, feedback shown

### Search (Algolia)
- [ ] Search input accessible
- [ ] Type query → results appear
- [ ] Clear query → results hide
- [ ] Tap result → goes to product

### Cart Dropdown
- [ ] Shows correct items/quantities/prices
- [ ] View cart link works
- [ ] Checkout link works
- [ ] Empty state shows when empty

### Cart Page
- [ ] All items display correctly
- [ ] Quantity toggle expands on mobile
- [ ] Increment/decrement works
- [ ] Remove item works, confirmation appears
- [ ] Subtotal correct
- [ ] Checkout button works
- [ ] Empty state displays when cart empty

### Checkout
- [ ] Page loads without error
- [ ] Stripe widget initializes and renders
- [ ] Form fields accessible
- [ ] Submit button visible
- [ ] Can complete test purchase (or verify widget functional)

### Contact Form
- [ ] Form renders, all fields visible
- [ ] Required validation triggers
- [ ] Can submit successfully
- [ ] Success feedback displays

### Gallery
- [ ] Images load
- [ ] Grid layout works (single column or appropriate)
- [ ] No horizontal overflow

### Turbo Navigation
- [ ] Navigate: Home → Products → Product → Cart → Checkout
- [ ] Use back button after each
- [ ] No JS errors, no stale content
- [ ] Cart state preserved throughout

### Edge Cases
- [ ] Empty cart page renders
- [ ] Visit invalid URL → 404 page
- [ ] Long product names don't break cards

---

## Breakpoint 2: Mobile XS Landscape (667px x 375px)

### Homepage
- [ ] Hero renders correctly in landscape
- [ ] No awkward cropping or overflow

### Navigation & Header
- [ ] Nav still works (hamburger or expanded)
- [ ] Cart dropdown positions correctly

### Products Index
- [ ] Grid adjusts (likely 2 columns)
- [ ] Cards don't stretch awkwardly

### Product Show
- [ ] Layout handles landscape orientation
- [ ] Image and details both visible

### Cart Page
- [ ] Layout handles wider viewport
- [ ] All controls accessible

### Checkout
- [ ] Stripe widget renders in landscape
- [ ] No clipping or overflow

### Contact Form
- [ ] Form usable in landscape

### Gallery
- [ ] Images display appropriately

---

## Breakpoint 3: Mobile SM Portrait (428px — iPhone 14 Pro Max)

### Homepage
- [ ] Hero renders correctly
- [ ] All elements fit

### Navigation & Header
- [ ] Hamburger or expanded nav works
- [ ] Cart dropdown works

### Products Index
- [ ] Grid layout appropriate
- [ ] Cards render well

### Product Show
- [ ] All content accessible
- [ ] Add to cart works

### Cart Page
- [ ] Items display correctly
- [ ] Quantity controls work
- [ ] Remove works

### Checkout
- [ ] Stripe widget renders
- [ ] All fields accessible

### Contact Form
- [ ] Form works

### Gallery
- [ ] Images render

### Turbo Navigation
- [ ] Full flow works without errors

---

## Breakpoint 4: Mobile SM Landscape (926px x 428px)

### Homepage
- [ ] Renders correctly

### Navigation
- [ ] Nav works (may be desktop nav at this width)
- [ ] Cart dropdown positions correctly

### Products Index
- [ ] Grid appropriate (2-3 columns)

### Product Show
- [ ] Layout works

### Cart Page
- [ ] Layout works

### Checkout
- [ ] Widget renders

### Contact Form
- [ ] Form works

### Gallery
- [ ] Images render

---

## Breakpoint 5: Tablet Portrait (768px)

### Homepage
- [ ] Hero renders, appropriate layout
- [ ] Navigation transitions (hamburger vs full nav?)

### Navigation & Header
- [ ] Desktop nav or hamburger — whichever is intended
- [ ] Cart dropdown works and positions correctly
- [ ] All nav links accessible

### Products Index
- [ ] Grid layout (2-3 columns expected)
- [ ] Cards sized appropriately

### Product Show
- [ ] Layout may be side-by-side image/details
- [ ] All content renders

### Search
- [ ] Desktop search experience (if different from mobile)
- [ ] Results display correctly

### Cart Dropdown
- [ ] Renders correctly at this width

### Cart Page
- [ ] Layout appropriate for tablet
- [ ] Quantity controls (desktop style now?)
- [ ] All functionality works

### Checkout
- [ ] Stripe widget renders
- [ ] Good use of space

### Contact Form
- [ ] Form layout appropriate
- [ ] All fields work

### Gallery
- [ ] Grid layout (2-3 columns)
- [ ] Images render well

### Turbo Navigation
- [ ] Full flow: Home → Products → Product → Cart → Checkout → Back
- [ ] No errors

---

## Breakpoint 6: Tablet Landscape (1024px x 768px)

### Homepage
- [ ] Full desktop-like experience
- [ ] Hero renders well

### Navigation
- [ ] Desktop nav visible
- [ ] Cart dropdown works

### Products Index
- [ ] Grid (3-4 columns)
- [ ] Cards render well

### Product Show
- [ ] Side-by-side layout likely
- [ ] Good use of space

### Cart Page
- [ ] Desktop layout
- [ ] All controls work

### Checkout
- [ ] Widget renders with good spacing

### Contact Form
- [ ] Desktop form layout

### Gallery
- [ ] Multi-column grid

---

## Breakpoint 7: Desktop (1280px)

### Homepage
- [ ] Full desktop experience
- [ ] Hero, images, CTAs all render
- [ ] Good use of whitespace

### Navigation & Header
- [ ] Full desktop nav visible
- [ ] All links work
- [ ] Cart icon and dropdown work
- [ ] Dropdown closes on outside click

### Products Index
- [ ] Grid (3-4 columns)
- [ ] Cards well-sized
- [ ] Hover states work (if any)

### Product Show
- [ ] Side-by-side layout
- [ ] Image gallery works (if multiple images)
- [ ] Add to cart works

### Search
- [ ] Desktop search works
- [ ] Results positioned correctly
- [ ] Clicking result navigates

### Cart Dropdown
- [ ] Positioned correctly
- [ ] All content visible
- [ ] Links work

### Cart Page
- [ ] Full desktop layout
- [ ] Item rows render correctly
- [ ] Quantity increment/decrement work
- [ ] Remove works with confirmation
- [ ] Subtotal correct
- [ ] Checkout button works

### Checkout
- [ ] Page loads
- [ ] Stripe widget initializes
- [ ] Good layout and spacing
- [ ] Can interact with all fields

### Contact Form
- [ ] Desktop layout
- [ ] Validation works
- [ ] Submit works

### Gallery
- [ ] Multi-column grid
- [ ] Images render at good size

### Turbo Navigation (Full Test)
- [ ] Home → Products
- [ ] Products → Product Show
- [ ] Product Show → Add to cart → Cart dropdown
- [ ] Cart dropdown → View Cart
- [ ] Cart page → Checkout
- [ ] Back button after each step
- [ ] Rapid click multiple nav links
- [ ] No JS errors in console
- [ ] No stale content anywhere
- [ ] Cart badge updates (KNOWN ISSUE)

### Edge Cases
- [ ] Empty cart page
- [ ] Empty cart dropdown
- [ ] No search results state
- [ ] 404 page
- [ ] Long product names
- [ ] Many items in cart (5+)

---

## Breakpoint 8: Desktop Large (1536px)

### Homepage
- [ ] Renders well, no awkward stretching
- [ ] Content centered or max-width contained

### Products Index
- [ ] Grid doesn't stretch too wide
- [ ] Cards appropriately sized

### Product Show
- [ ] Layout handles extra width

### Cart Page
- [ ] Layout contained

### Checkout
- [ ] Widget centered/contained

### Contact Form
- [ ] Form doesn't stretch awkwardly

### Gallery
- [ ] Grid handles width well

---

## Known Issues Checklist

Verify these specific bugs from code exploration:

- [ ] Quantity input: test incrementing past reasonable max (no constraint exists)
- [ ] Cart badge: add item, check if header badge updates without page refresh
- [ ] Cart dropdown: remove last item, verify empty state appears
- [ ] Checkout loading: note if there's a blank/loading period before Stripe renders
- [ ] Contact form: submit empty, note if error styling matches design
- [ ] Cart remove: verify confirmation dialog appears and works

---

## Bugs Found During Testing

| Breakpoint | Page/Flow | Description | Severity | Pre/Post MVP |
|------------|-----------|-------------|----------|--------------|
| | | | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |

## Notes
-
-
-
