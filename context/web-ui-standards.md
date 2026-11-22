# Web UI coding standards

Apply this guide to code that renders HTML in a browser, including HTML generated from JSX or templates. Use it alongside `context/coding-standards.md` for any request affecting that output. Paths in this guide are relative to the project root.

## Semantics and accessibility

- Use semantic HTML in the rendered output. Use buttons for actions, links for navigation, and logical headings and landmarks. Label controls, support keyboard operation, and provide visible focus. Verify the accessible names, keyboard operation, and focus behavior of changed controls. [MDN HTML accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/HTML)

## Frontend stack and performance

- Identify the frontend stack, installed versions, and rendering or build setup from the repository. Follow the Context7 workflow in `AGENTS.md` to look up patterns for the specific change, including web platform APIs and framework conventions where applicable.
- Keep content needed for the initial view and primary interaction readily available. Consider deferring substantial, noncritical code or media when it reduces initial work without an undue delay when the user needs it. Keep the image expected to drive Largest Contentful Paint (LCP) out of lazy loading. [Optimizing LCP](https://web.dev/articles/optimize-lcp)
- Use the framework's documented route or component splitting when it fits the app. For browser-rendered React, a substantial UI that opens on demand can use `lazy` at module scope with a `Suspense` fallback. Check when the deferred chunk loads and how the interaction behaves while it loads. [React lazy](https://react.dev/reference/react/lazy)
- For changes that can materially affect loading or rendering, measure the relevant result with existing checks or browser tools. Use a production build where possible and the same route and conditions for before-and-after comparisons. Match the metric to the change, such as initial JavaScript bytes for splitting, LCP for page load, or a rendering profile for slow updates. Report measured results and any checks that could not run. [React Profiler](https://react.dev/reference/react/Profiler)

## Browser verification

- Exercise the affected flow in a browser at representative narrow and wide viewports and cover applicable states from the spec. Use Playwright MCP when configured and a built-in browser is unavailable.
