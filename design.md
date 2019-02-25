# Progressive Hydration

Universal Rendering, or what developer avocados call it **SSR**, achieves a fast First Contentful Paint. Server-Side renders application to HTML and embeds application state in the resulting document. Then, Client-Side is required to pick up from where Server-Side left using a technique called [(re)hydration](#def-rehydration).

SSR with rehydration achieves fast [TTFB](#def-ttfb) and [FCP](#def-fcp) but suffers from slow [TTI](#def-tti). Rehydrating incrementally or partially is a key technique making SSR achieve fast [TTI](#def-tti). Incremental and partial rehydration is termed as **Progressive Hydration**.

## Goals

1. **Benefits of progressive hydration:**
    Create same webpage with and without progressive hydration.

1. **Triggers for hydration:**
    [(re)hydration](#def-rehydration) can be started by different conditions depending on type of content.
    1. _On interaction:_
        User interactions like clicking, hovering or focusing require [(re)hydration](#def-rehydration) to work as expected and these interactions are real triggers for [(re)hydration](#def-rehydration).
        _On interaction [(re)hydration](#def-rehydration)_ works really well when the DOM tree being hydrated can complete under 16ms.

        The magic number 16ms (1 frame = 16ms) comes from 60fps rendering goal. If [(re)hydration](#def-rehydration) can be completed in 1 frame, the experience would be same as already hydrated DOM tree. This limit can be relaxed to a couple of frames as the difference would be unnoticeable.

    1. _When visible:_
        _On interaction [(re)hydration](#def-rehydration)_ is a heuristic approach depending on the constraint that the requested DOM tree can be hydrated in under 1 frame but we can never ensure 1 frame constraint as device can have slow processor or degraded performance due to unexpected load/low battery etc. An improvement would be hydrating when a DOM tree enters visible area.

    1. _When idle:_
        _[(re)hydration](#def-rehydration)_ can be started when CPU is free. This technique would progressively hydrate full DOM tree without user interaction. Visually, it is same as normal _[(re)hydration](#def-rehydration)_ but [TTI](#def-tti) is improved significantly as it's not hydrating all at once.

    1. _SSR only:_
        If a DOM sub-tree does not have any interaction, then there are no benefits of _[(re)hydration](#definition-rehydration)_.

    1. _Controlled:_
        Sometimes we get to know at runtime when _[(re)hydration](#definition-rehydration)_ is required, for such scenarios an explicit trigger can be used.

    1. _Scheduled:_
        When using _when idle [(re)hydration](#definition-rehydration)_, it uses `requestIdleCallback`. If the `requestIdleCallback` API is not available, it has to fallback to `setTimeout` which indeed is scheduling _[(re)hydration](#definition-rehydration)_.

## Solution

A webpage with charts using data from Github vuejs organization.

<!-- markdownlint-disable MD033 -->

## Terminology

<dl id="definitions">
  <dt id="def-fcp">FCP</dt>
  <dd>First Contentful Paint - the first time any pixel gets becomes visible to the user</dd>
  
  <dt id="def-ttfb">TTFB</dt>
  <dd>Time to First Byte - seen as the time between clicking a link and the first bit of content coming in.</dd>
  
  <dt id="def-tti">TTI</dt>
  <dd>Time to Interactive - the time at which a page becomes interactive (events wired up, etc).</dd>
  
  <dt id="def-rehydration">(re)hydration</dt>
  <dd>"booting up" JavaScript views on the client such that they reuse the server-rendered HTML’s DOM tree and data.</dd>
</dl>

<!-- markdownlint-enable MD033 -->
