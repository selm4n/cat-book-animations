# Yarn Pounce: measurements

Measured on 2026-09-25 (local date; 2026-09-26 03:16 UTC) in Chromium 153.0.0.0 on Windows x64, 16 reported logical processors, DPR 1. Browser viewport: 1000 × 800; one illustration: 480 × 320. The tab remained foreground. No CPU/network throttling was applied. [Raw observations](measurements.json) are included.

## Weight

Bytes were counted from the UTF-8 files, without minifying. Gzip values were calculated with Node's built-in zlib.gzipSync at level 9; these are encoded byte sizes, not a claim about server compression settings. The component CSS includes both timings and reduced-motion support. Demo typography and controls are excluded from the reusable-component rows.

| Payload | Raw bytes | Gzip bytes |
| --- | ---: | ---: |
| Inline figure (play-once) | 1,827 | 901 |
| Component CSS, both timing variants | 6,415 | 1,132 |
| Figure + component CSS, compressed together | 8,243 | 1,957 |
| Play-once demo HTML + full demo CSS, compressed separately | 13,739 | 4,054 |
| Loop demo HTML + full demo CSS, compressed separately | 13,759 | 4,062 |

The figure+CSS row contains a single newline between the strings. A separately linked component stylesheet compresses separately: 901 + 1,132 = 2,033 gzip bytes. No script, font, image, or dependency payload is requested by the component. README and measurement files are not runtime assets. Its line weight is 2.6 SVG units, identical to study 01.

## Layout shift

**Observed CLS: 0** for every sample and across the full measurement session, including the initial page load. An isolated fixed-size slot hosted the actual component SVG/CSS, with no demo text or embedded fonts. A buffered PerformanceObserver captured layout-shift entries; CLS used the maximum session-window sum, excluding recent-input entries. The SVG retains its intrinsic width/height and 3:2 aspect ratio while internal groups move or fade.

This establishes zero shift in this fixture. It is not a guarantee for an arbitrary host page: removing the dimensions, late-sizing the parent, or changing unrelated content can cause CLS. Keep the reserved aspect ratio when embedding.

## Main-thread observations

Three 10-second samples per mode, interleaved static → play-once → loop. Static used the same figure with animation:none; play-once included its 4.8-second action and approximately 5.2 seconds holding the final pose. Loop covered more than one complete 7.2-second cycle per sample. Observers and requestAnimationFrame sampling lived in a temporary measurement page, not in the shipped animation or demos.

| Mode (3 × 10 seconds) | Long tasks >50 ms | Long-task duration | Long animation frames >50 ms | LoAF blocking time | Median / p95 rAF interval |
| --- | ---: | ---: | ---: | ---: | --- |
| Static baseline | 0 | 0 ms | 0 | 0 ms | 16.7 / 16.8 ms |
| Play once | 0 | 0 ms | 0 | 0 ms | 16.7 / 16.8 ms |
| Loop | 0 | 0 ms | 0 | 0 ms | 16.7 / 16.8 ms |

All nine samples had zero rAF intervals above 34 ms. The browser advertised support for layout-shift, longtask, and long-animation-frame observers. The per-trial timings and counts are in measurements.json.

**These are measured main-thread blocking and frame-cadence observations, not total main-thread CPU time.** The Long Tasks/Long Animation Frames APIs omit shorter work; 0 ms here does not mean no style, paint, compositing or CPU cost. Total sub-50-ms rendering time and compositor/GPU time were not captured. A browser performance trace on the intended device is needed for a total CPU-cost figure. No claim that SVG transforms are always compositor-only is made.

## Verification and reproduction

- Compared the fourth cat's path data to study 01: unchanged geometry and proportions. Existing studies' HTML/CSS remained byte-identical.
- Sampled both CSS timelines, including the edge reset; loop and play-once reach the same final transforms at 4.8 seconds.
- Advanced play-once to 12 seconds: still the same visible final pose, with no restart.
- Activated the production reduced-motion declarations in a browser fixture: no animations; base coordinates form the complete resting drawing. This tested the declarations, not a change to the operating-system preference.
- Checked reserved proportions, inherited dark/white/green colors, transparency, and the 2.6-unit stroke in the browser. The small fixture included 160px-wide output.

To repeat the timing measurement, place only the copied figure and component CSS in a 480px-wide slot on a blank page. Attach buffered PerformanceObservers for layout-shift, longtask and long-animation-frame before rendering. Record requestAnimationFrame timestamps in the same fixture. Run three 10-second trials for each mode, in the order above, keeping the tab foreground. Aggregate only entries whose startTime falls within each trial; report the static baseline too. Do not add this instrumentation to the reusable component. For total main-thread work, record a Performance trace covering those same intervals and report scripting, style/layout and paint separately.
