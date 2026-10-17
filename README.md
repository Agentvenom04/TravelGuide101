# Responsive images

Every image on the site uses a responsive technique, chosen by what the image does on the page.

## Summary

| Image | Pages | Technique |
|---|---|---|
| Hero image | All 5 pages | `<picture>` + `<source media>` |
| Feature cards | Home | `srcset` + `sizes` |
| Property listings | Explore homes | `srcset` + `sizes` |
| Service cards | Services | `srcset` + `sizes` |
| Story image and team portraits | About | `srcset` + `sizes` |
| Decorative backgrounds | — | Not used (no CSS background images) |

## Hero image: `<picture>` and `<source>`

```html
<picture>
  <source media="(max-width: 600px)" srcset="...w=720...">
  <source media="(min-width: 601px)" srcset="...w=1400...">
  <img class="hero-image" src="...w=1400..." alt="..." fetchpriority="high">
</picture>
```

**Why this technique:** the hero changes layout between mobile and desktop.

- On desktop it sits next to the text as a wide, 330px-tall crop, so it needs a large 1400px file.
- At 600px and below it stacks under the text in a 4:3 frame, so a 720px file is enough.

`<picture>` lets us tie each file to a breakpoint from the stylesheet (`max-width: 600px`), the same point where the layout changes. The `<img>` inside is the fallback for browsers that don't support `<picture>`, and it carries the alt text.

It also uses `fetchpriority="high"` because it's the first thing visible, and no `loading="lazy"`, so it's never delayed.

## Content images: `srcset` and `sizes`

```html
<img src="...w=700..."
     srcset="...w=350... 350w, ...w=700... 700w"
     sizes="(max-width: 360px) calc(100vw - 28px), (max-width: 600px) calc(50vw - 25px), (max-width: 800px) 310px, 260px"
     alt="..." loading="lazy">
```

**Why this technique:** these images show the same photo, crop and shape at every screen size. Only the display width changes. That's the case `srcset` + `sizes` is made for.

- `srcset` lists the available files and their real widths.
- `sizes` tells the browser how wide the image will display at each breakpoint. The values match the card widths set in `style.css`.
- The browser combines the display width with the screen's pixel density and downloads the smallest file that still looks sharp.

| Image | Display width (`sizes`) | Files |
|---|---|---|
| Home feature cards | 260px desktop, 310px tablet, half the screen on mobile, full width below 360px | 350w, 700w |
| Explore listings and Services cards | 340px desktop, 45% of the screen on tablet, full width on mobile | 400w, 800w |
| About team portraits | 260px desktop, 45% of the screen on mobile | 300w, 600w |
| About story image | 500px on wide screens, 45% of the screen below 1128px, full width on mobile | 480w, 800w, 1200w |

They all use `loading="lazy"` because they're below the first screen, so the browser only loads them when the visitor scrolls near them.

**Measured in Chrome (1.5× display):**

| Screen width | Home feature card | Explore listing |
|---|---|---|
| 1280px | 248px wide → 350w file (was 700w) | 343px wide → 400w file (was 900w) |
| 768px | 305px wide → 350w file | 344px wide → 800w file |
| 375px | 151px wide → 350w file | 323px wide → 800w file |

## No stretching or distortion

The stylesheet makes every image fit its container without changing its proportions:

- `img { max-width: 100%; height: auto; }`: an image can never be wider than its container, and its height follows its width.
- Cards and heroes set a fixed shape with `aspect-ratio` (1:1, 4:3 or 16:10) or a fixed height, and the image uses `object-fit: cover`. The photo is cropped to fill the frame instead of being squashed.
