[README.md](https://github.com/user-attachments/files/33590875/README.md)
# E & B. — Real Estate Landing Page

A responsive, single-page real estate landing page inspired by the customer supplied layout reference.


## Requirements covered

- Semantic HTML5 sections, navigation, main content, articles, blockquote, and footer.
- Vanilla CSS in the external `style.css` file; no JavaScript and no CSS Grid.
- Flexbox for the header, hero, feature cards, CTA, and footer.
- Responsive media queries for mobile, tablet, and desktop layouts.
- Roboto imported from Google Fonts.
- CSS-only mobile burger menu using a checkbox and label.
- Responsive images with `max-width: 100%`, `object-fit: cover`, lazy loading for below-the-fold photos, and a `<picture>` element for the hero image.

## Responsive image technique

The hero uses `<picture>` with media-specific image URLs so smaller screens can request a 720-pixel-wide image while larger screens can request a 1400-pixel-wide version. This is appropriate for the hero because it is the largest visual on the page and benefits from a larger source on desktop while reducing image transfer on mobile. The browser chooses the matching `<source>` based on the viewport; the nested `<img>` remains a fallback and provides meaningful alt text. The property cards use regular `<img>` elements with `width: 100%`, `height: 100%` inside a square aspect-ratio frame, and `object-fit: cover`, so they fill their frames without stretching. Their `loading="lazy"` attributes defer loading until the images are near the viewport.

## Pages
- `index.html` — main landing page
- `explore.html` — property listing page
- `contact.html` — contact details page
- `services.html` — services offered  page
- `about.html` — about the company page
- `style.css` — shared styles and responsive page styles
