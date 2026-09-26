# Cat & books

A minimal collection of reusable SVG cat animations for web interfaces. Cats turn small stacks of books into places to perch, peek, and play. The artwork uses one inherited color, a transparent background, and gentle CSS motion.

## Preview
Open index.html directly in a modern browser to see the gallery. Choose Dark line, Light line, or Muted green to see color inheritance. Pause motion freezes all previews at their current position. Select a card to open its standalone demo. No installation or build step is required.

## The collection
| Variation | What happens | Loop | Suggested use |
| --- | --- | --- | --- |
| [Cat on Book Stack](01-cat-on-book-stack/index.html) | A perched cat looks down and taps a bookmark | 8s | Under a heading, beside a paragraph |
| [Cat Between Books](02-cat-between-books/index.html) | Ears and a face rise between books, followed by a paw and tail | 9s | Section edge, footer, loading state |
| [Yarn Across the Books](03-yarn-across-books/index.html) | Yarn arrives first; the cat follows, climbs slightly and taps it | 8s | Hero, section divider |
| [Yarn Pounce](04-yarn-pounce/index.html) | Yarn rolls in; a cat pounces and settles with a paw on it | 7.2s loop / [4.8s once](04-yarn-pounce/once.html) | Section accent, hero |

## Embed an animation
1. Copy figure.cat-book-animation from a standalone index.html into your page. Keep its variation class.
2. Copy the component rules from style.css, up to the Demo presentation comment. Include those rules once, even when combining different variations.
3. Size and color the surrounding container as needed.

The first three component stylesheets contain the same shared rules. Study 04 has its own scoped component rules; include its CSS as well when combining it with earlier studies. The gallery contains its own inline previews and can run without iframes or scripts. CSS selectors and keyframe names are scoped; no SVG IDs, remote resources or dependencies are used. The gallery.css stylesheet includes all four studies. No empty script files are included.

## Change color

```css
.cat-book-animation { color: #1f1f1f; }
```

The entire illustration inherits this value through currentColor. It also inherits the parent text color when no explicit color is set. White works on dark sections; dark brown, navy and brand colors work equally well. For the third variation only, --cba-yarn-color may supply an optional second color. Its default is currentColor.

## Change size

```css
.cat-book-animation { width: 100%; max-width: 400px; }
```

The 480 × 320 SVG viewBox preserves the composition without distortion. Use container widths of approximately 160–800px. The illustration does not assume a full-screen layout or fixed screen position.

## Transparent background
There is no painted background, opaque background fill, gradient, texture or shadow inside the component. Nested SVG clipping lets the second cat hide behind books without depending on a page background color. The gallery's preview surfaces belong to the demo UI only.

## Motion and accessibility
All motion is SVG/CSS; JavaScript is unnecessary. Studies 01–03 share each instance's --cba-duration variable; study 04 uses coordinated 4.8-second and 7.2-second timelines. Small gestures are separated by moments of stillness. The traveling scene resets beyond the viewport; the other scenes return to their starting pose.

With prefers-reduced-motion:reduce, every animation is disabled and all four cats remain visible in a composed static state. The figure has an accessible description. If the art is purely decorative, remove its role and aria-label and set aria-hidden="true". The preview color and pause controls use native form controls and CSS :has(), supported in current browsers.

See each variation's README for its placement and customization notes.

## Study 04: playback and performance

Yarn Pounce reuses the original 2.6-unit cat drawing. Its default is a 4.8-second play-once animation that holds a composed resting pose; cba-pounce--loop selects the 7.2-second gallery loop. The reduced-motion drawing matches the final pose. See [study 04](04-yarn-pounce/README.md) for embedding and [measured performance](04-yarn-pounce/PERFORMANCE.md) for raw/gzip weight, layout-shift observations and main-thread measurement limits.
