# CF Consulting Services Corp | Website

Four static pages built on the Minimalist Modern design system. No build step, no framework, no npm install. Push it to GitHub Pages and it runs.

```
index.html                     Home
dl4-administration.html        Service page 01
aws-cloud-architecture.html    Service page 02
contact.html                   Discovery Audit request
styles.css                     Design tokens plus all component styles
script.js                      Entrance animations and mobile nav
```

## How the design system is implemented

The system doc describes a React and Tailwind setup with a StyleWrapper injecting CSS custom properties and Framer Motion driving animation. This site is static HTML on GitHub Pages, so the same architecture is expressed with the platform's own primitives:

| Design system concept | Implementation here |
|---|---|
| Design tokens via StyleWrapper | CSS custom properties in a single `:root` block at the top of `styles.css`. Every color, shadow, radius, font, and easing curve is declared once. Nothing below `:root` hardcodes a hex value. |
| `cva` component variants | Class composition, for example `.btn` plus `.btn-primary` plus `.btn-lg`. Same mental model, no dependency. |
| Framer Motion entrance animations | IntersectionObserver adds an `.in` class. `.reveal` fades a block up, `.stagger` cascades its children at 100ms intervals. Duration 700ms on the system's `cubic-bezier(0.16, 1, 0.3, 1)` curve. |
| Continuous motion | CSS keyframes: 72s ring rotation, 4s and 5s card bobbing at 10px amplitude, 2s badge pulse. |

If this later moves to React, the token block ports over unchanged and the class names map cleanly onto component variants.

## Where the "bold factor" elements live

1. **Gradient text with underline bar** on the last word of each page headline.
2. **Inverted sections** using `--foreground` as background, with the 32px dot pattern at 3% opacity. Home uses two: the process timeline and the stats band.
3. **Animated hero composition**: rotating dashed ring with an accent node, two floating cards showing decision engine and engagement state, a 3x3 dot grid, and a gradient corner badge. Hidden below 1024px per the responsive strategy.
4. **Gradient icon backgrounds** on the two service cards, scaling to 110% on hover.
5. **Gradient border stroke** on the featured Tier 2 pricing card, which also floats above its siblings.
6. **Section label badges** with a pulsing accent dot open every major section.
7. **Asymmetric grids**: hero at `1.1fr 0.9fr`, service page split at `1.2fr 0.8fr`, and a `4rem` top left radius on the aside cards.

## Accessibility

- Skip link to main content on every page.
- Focus rings use `ring` token at 2px with 2px offset, visible on every interactive element.
- All buttons are 48px or 56px tall, above the 44px touch target minimum.
- Mobile nav toggles `aria-expanded`, closes on Escape, and returns focus to the button.
- `prefers-reduced-motion` disables the rotating ring, floating cards, pulsing dots, hover lifts, and entrance animations.
- Current page marked with `aria-current="page"` and a gradient underline.
- Decorative SVG and layout elements are `aria-hidden`.

## Deploy to GitHub Pages

1. Push all six files to the root of a repo on `main`. Keep them in the same folder, the links are relative.
2. Settings, then Pages, then Source, then Deploy from a branch, branch `main`, folder `/ (root)`.
3. Live at `https://yourusername.github.io/reponame/` within about a minute.
4. For a custom domain: add it under Settings, then Pages, then Custom domain, add a CNAME record at your registrar, and check Enforce HTTPS once it verifies. GitHub provisions the certificate for free.

## Before launch

- **Contact form endpoint.** `contact.html` posts to a placeholder Formspree URL containing `YOUR_FORM_ID`. Create a form at formspree.io and swap in the real endpoint. Until then the mailto link to info@CFCS.com is the working path, so no lead is lost.
- **Client logos.** The four names on the home page render as styled text, not logo artwork. Before launch, confirm each company was a client of this entity, get sign off that you can name them, then replace the wordmark span with an image:
  ```html
  <div class="logo-tile"><img src="assets/logos/ironhorse.svg" alt="Ironhorse Funding"></div>
  ```
  Worth being deliberate about Lincoln Financial Group and Evercore Partners in particular. They are large, visible firms, a prospect can verify the claim, and some companies have policies against being listed.
- **Pricing visibility.** The BRD flags this as open. Published ranges build trust and filter unqualified inquiries, but they also give MeridianLink a number to undercut. If you would rather gate it, delete the tier grid sections and the pricing note lines, and the pages still read complete.
- **Analytics.** Nothing is wired in. The BRD's success metrics need inbound inquiry tracking, so add something light like Plausible or GoatCounter.
- **Favicon and social preview image.** Not included. Worth adding an `og:image` before this link goes out on LinkedIn.
