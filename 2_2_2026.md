## how to find a memory leak in the wild w/ DevTools

1. Performance Monitor (quick check)
- DevTools > ... Menu > More tools > Performance Monitor
- watch "JS heap size" as you navigate around the page
- if it keeps climbing & never drops, that's a mem leak

2. Memory tab (deeper analysis)
- DevTools > Memory tab
- Take a "Heap snapshot" BEFORE navigating around the page
- Navigate around the site for awhile
- Take another snapshot
- Compare them: look for objects that keep growing in count

3. Performance tab (event listener leaks)
- Record a session while navigating
- Look for increasing numbers of listeners or DOM nodes

Quick practical test:
1. Open DevTools > Memory tab
2. Click "Collect garbage" button [trash icon] to establish baseline
3. Note the memory number
4. NAvigate around the site 10-15 times
5. Click "Collect garbage" again
6. Compare - if memory is significantly higher and won't drop, something's leaking


