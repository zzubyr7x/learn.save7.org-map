# Save7 Brand Assets

Source of truth: https://save7.org/brand-kit#files (page's own words: "Keep this page bookmarked — it is the single source of truth for Save7 brand files.")

## Files (all PNG, copied from the brand-kit page)

- `Save7-logo-stacked.png` (1201×585) — default lockup: covers, hero banners, signage
- `Save7-logo-horizontal.png` (2182×273) — tight/wide spaces: app bars, headers, banners
- `Save7-V7-mark.png` (1385×1291) — icon mark only: favicons, avatars, small formats
- `Save7-V7-with-url.png` (1473×1570) — mark + save7.org, no wordmark: posters, stickers
- `Save7-V7-with-type.png` (1473×1570) — full lockup: mark + SAVE7 wordmark + save7.org
- `Save7-social-overlay.png` (900×1600) — transparent social post template; don't recolor/reposition

## Palette

> **These tokens disambiguate the brand-kit page; they do not mirror it.**
> The brand-kit page is not single-valued — it carries both `#ED0E69` and
> `#df0e62` (plus `#d00a5c` / `#c40c58`), and names three typefaces. The
> values below are the resolved set for Save7 web properties, chosen on
> measured WCAG contrast. Please don't "correct" them back to the
> brand-kit page's first-listed values — see the reasoning below.

| Token | Hex | Use |
|---|---|---|
| `pink` | `#df0e62` | Hero colour. **4.80:1 on white — clears WCAG AA for normal text.** Safe for headings, links and CTA labels at body size on white. Large text only on ink (3.94:1). |
| `teal-on-ink` | `#16B9B4` | The true brand teal. 7.76:1 on ink — AAA. **Never on white** (2.43:1). |
| `teal-on-white` | `#00807B` | Teal for white surfaces. 4.80:1 — AA for normal text, matching the pink. |
| `white` | `#FFFFFF` | Default background |
| `ink` | `#111111` | Text & dark surfaces (18.88:1 on white) |

### Why two teals

No single colour can clear AA for normal text on **both** white and
`#111111`: clearing 4.5:1 on white requires relative luminance ≤ 0.185,
and clearing it on ink requires ≥ 0.20. The constraint is the *surface*,
not the role — so the accent that gets read at body size needs one token
per surface, and the token name carries the constraint so there is no
prose rule left to forget.

`#00918C` (used elsewhere in Save7 OS) is **not** safe for body-size text
on white: it measures 3.87:1, large-text-only. It is fine on ink (4.88:1).

### Superseded

`#ED0E69` was the previously recorded hero pink here. It measures 4.31:1
on white and **fails** AA for normal text. `#df0e62` replaces it — it is
also the incumbent `--color-primary` on the live save7.org Astro site.

## Typography

Two typefaces, no exceptions (both on Google Fonts):

- **Lexend** — body, UI, captions. This is `--font-sans` on the live
  save7.org site; Learn matches it for consistency across Save7 web
  properties.
- **Anton** — display only: headlines and numbers, all-caps, tight, loud.
  Never for body copy.

**Inter is dropped.** It was previously recorded here as the body face,
but the running site uses Lexend and the brand-kit page lists all three.
Two faces survive into Learn: Lexend + Anton.

## Tailwind v4 note

Tailwind is used for consistency with the sibling Astro site, **not** for
enforcement. Enforcement is a separate, explicit act — in `@theme`:

```css
@theme {
  --color-*: initial;   /* drop Tailwind's default palette entirely */

  --color-pink: #df0e62;
  --color-teal-on-ink: #16B9B4;
  --color-teal-on-white: #00807B;
  --color-white: #FFFFFF;
  --color-ink: #111111;

  --font-sans: "Lexend Variable", sans-serif;
  --font-display: "Anton", sans-serif;
}
```

Without the `--color-*: initial` reset the default palette stays live.
That is how the existing save7.org site went from four colours to nine —
its compiled CSS currently emits `indigo-600`, `emerald-700`,
`orange-700`, `sky-600/700/800`, `cyan-900`, `red-500` and
`pink-300/900` alongside the brand tokens, because Tailwind v4 emits a
`--color-*` custom property for every utility actually used in the build.
