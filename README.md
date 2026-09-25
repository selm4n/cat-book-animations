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

## Embed an animation
1. Copy figure.cat-book-animation from a standalone index.html into your page. Keep its variation class.
2. Copy the component rules from style.css, up to the Demo presentation comment. Include those rules once, even when combining different variations.
3. Size and color the surrounding container as needed.

All three component stylesheets contain the same shared rules. The gallery contains its own inline previews and can run without iframes or scripts. CSS selectors and keyframe names are scoped; no SVG IDs, remote resources or dependencies are used. The only extra root stylesheet is gallery.css. No empty script files are included.

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
There is no painted background, opaque fill, gradient, texture or shadow inside the component. Nested SVG clipping lets the second cat hide behind books without depending on a page background color. The gallery's preview surfaces belong to the demo UI only.

## Motion and accessibility
All motion is SVG/CSS; JavaScript is unnecessary. Keyframes share each instance's --cba-duration variable. Small gestures are separated by moments of stillness. The traveling scene resets beyond the viewport; the other scenes return to their starting pose.

With prefers-reduced-motion:reduce, every animation is disabled and all three cats remain visible in a composed static state. The figure has an accessible description. If the art is purely decorative, remove its role and aria-label and set aria-hidden="true". The preview color and pause controls use native form controls and CSS :has(), supported in current browsers.

See each variation's README for its placement and customization notes.
