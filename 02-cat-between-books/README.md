# Cat Between Books

A cat peeks up between upright and horizontal books, looks around, reaches a paw over a book and lowers again.

Part of a minimal collection of reusable SVG cat animations for web interfaces.

## Files and preview
- index.html: standalone demo and inline SVG component.
- style.css: component rules, followed by clearly marked demo presentation.
- README.md: embedding and customization instructions.

Open index.html directly in a current browser. There is no build step, server, dependency, JavaScript or separate asset. The gallery is ../index.html.

## Embed
Copy the complete figure.cat-book-animation element from index.html. Copy the component CSS from style.css, stopping before the Demo presentation comment. Keep the cba-between class. These component rules support all three variations; include them only once if combining scenes. There are no SVG IDs to collide when repeating instances. Every selector and keyframe is scoped or prefixed.

## Color
The illustration inherits the container's color. For example:

```css
.cat-book-animation { color: #1f1f1f; }
```

Set color to white, navy, a brand color or any other CSS color.  No background-colored shapes or masks are used. The demo surface is outside the reusable figure.

## Size
The 480 × 320 viewBox scales proportionally from about 160px to 800px wide. Set width or max-width on the figure or its parent.

```css
.my-cat-slot { width: min(100%, 400px); color: navy; }
```

Suggested use: section edge · footer · loading state. The component has no fixed screen positioning.

## Motion
A 9-second cycle uses coordinated CSS keyframes with quiet pauses. Change --cba-duration on this instance to adjust the full timeline. Under prefers-reduced-motion:reduce, all motion stops and the cat remains visible in its resting coordinates.

For decorative use, replace role="img" and aria-label on the figure with aria-hidden="true". Otherwise keep the descriptive label. The demo's native radios and pause checkbox are keyboard accessible and use CSS :has(); no script is required. If adding your own pause control, set animation-play-state:paused on descendants of this figure and running to resume.
