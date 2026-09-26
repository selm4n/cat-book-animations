# Yarn Pounce

A yarn ball rolls in from the right edge and comes to rest. The same cat used in Cat on Book Stack follows in a small pounce, bats the yarn, then settles with one paw resting on it.

## Preview and timing

- **index.html** — 7.2-second loop: the same 4.8-second action, a composed hold, and a short fade. The next arrival starts beyond the clipped viewport.
- **once.html** — 4.8-second play-once version. It finishes in a visible resting pose and holds it using animation-fill-mode:both. Reload to replay.
- **style.css** — reusable component rules, followed by demo presentation.
- **README.md** — use and measurement notes.
- **PERFORMANCE.md**, **measurements.json** — measurement method, results and raw observations (not loaded by the animation).

Open either HTML file directly. No server, build step, JavaScript, external dependencies, fonts or images are required.

## Construction

The original cat geometry is reused from study 01 without scaling or redrawing its proportions. The line system is the same 2.6 SVG-unit stroke with round joins and caps in a 480 × 320 viewBox. Every drawn line uses currentColor. The small nose fill also follows currentColor, as in studies 01 and 02. All motion uses CSS transform and opacity keyframes; no geometry, layout properties or path data are animated.

## Embed

Copy figure.cat-book-animation from once.html and the component portion of style.css, stopping before the Demo presentation comment. This is the play-once default. Add **cba-pounce--loop** for continuous playback. Do not override only the duration: the loop has its own synchronized offsets so the first 4.8 seconds match the play-once action.

The fourth study's CSS is standalone. Include it in addition to the earlier studies' CSS when combining components; its selectors and names are scoped to cba-pounce. All SVG groups are inline, with no IDs or asset requests. No script.js file is needed.

Set color on the figure or its parent to recolor the entire drawing. Set width or max-width to size it; 160–800px is the intended range. The SVG has explicit 480 × 320 width/height attributes and a 3:2 CSS aspect ratio to reserve its slot. Keep these when embedding.

The component background is transparent, including the inside of the cat and yarn. The demo's preview surface is outside the figure. There are no opaque masks, shadows or gradients.

## Accessibility and resting pose

The unanimated SVG is itself the final pose: cat settled, paw touching the top of the yarn. prefers-reduced-motion:reduce removes every animation and shows that pose immediately, without an entrance or fade. The play-once final transforms match those same base coordinates. Animating the loop's opacity does not remove the reserved layout box.

Keep the figure's descriptive accessible label when the illustration conveys meaning. For decoration, remove role and aria-label and use aria-hidden="true" instead. The demo color and pause controls use native inputs and CSS :has(). Pausing freezes the current pose; it does not restart the animation.

## Measurements

Measured transfer weight, layout shift and main-thread observations are recorded in [PERFORMANCE.md](PERFORMANCE.md), with the browser, sample duration and limits of the measurements. CSS-only does not mean zero browser CPU cost.

Measured reusable payload: **8,243 bytes raw / 1,957 bytes gzip** (figure and component CSS compressed together). At 480px wide in Chromium 153, three 10-second trials per mode recorded **CLS 0**, **0 long tasks over 50 ms**, and **0 long animation frames**, matching the static baseline. These measurements do not quantify total sub-50-ms rendering CPU; see the performance notes for that limit and raw data.
