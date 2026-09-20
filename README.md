# FalseType

yet another pixel-perfect font. pun on truetype cause it's not anti-aliased.

![Charset preview](glyphs/charset-preview@8x.png)

## Use

Copy `dist/FalseType.woff2` into your site and size it in whole rem:

```css
@font-face {
  font-family: 'FalseType';
  src: url('/fonts/FalseType.woff2') format('woff2');
  font-weight: 100 900; /* one face answers every weight */
  font-display: block;
}

.logo {
  font-family: 'FalseType', monospace;
  font-size: 2.25rem; /* whole multiples of 0.75rem: 12px is 1:1, 24px 2:1, 36px 3:1 */
  line-height: 1;
  letter-spacing: 0;
  font-kerning: none;
  font-synthesis: none; /* no faked bold or italic; both render as regular for now */
}
```

There is one face. Browsers fake bold by smearing and italic by shearing, which puts every pixel
between two others, so turn synthesis off and bold or italic text renders regular until those glyphs
exist.

One canvas pixel is 100 units of a 1200 unit em, so the em is 12 canvas pixels: 10 above the
baseline and 2 below. Caps are 8 pixels, two thirds of the em like Arial or Archivo, so FalseType at
a size looks about as big as a text face at that size, and with `line-height: 1` its baseline lands
where theirs does. x-height is 5, descenders 3, and every letter advances its width plus 1.

Pixel-perfect sizes are whole multiples of 12px: 0.75rem, 1.5rem, 2.25rem, 3rem. Anything else, or a
browser zoomed to anything but 100%, puts the pixels off the device grid and blurs them. Descenders
reach one canvas pixel below the em and accents on capitals one above it; a container with
`overflow: hidden` needs `overflow: clip; overflow-clip-margin: 0.25em` instead so they survive.

## Charset

Printable ASCII, Latin-1 letters plus Œ œ Š š Ž ž Č č Ÿ, typographic punctuation, `€ £ ¥ ¢`,
arrows `← → ↑ ↓ ↔`, checks `✓ ✔ ✗ ✘`, stars `★ ☆` and hearts `♥ ♡`. No kerning table yet.

## Edit

The letters A to Z and a to z are copied from the canvas. Everything else lives as text bitmaps in
`glyphs/extra-glyphs.mjs`:

- `EXTRA_GLYPHS` are drawn glyphs, rows top to bottom in an 11 row frame that starts at the cap top,
  `#` for ink.
- `COMPOSED` builds accented letters from a base letter and a mark in `MARKS`. A bitmap in
  `EXTRA_GLYPHS` for the same character wins, which is how you override a composed shape.

Then rebuild:

```sh
npm install
npm run build
```

`build:sheet` rewrites `glyphs/sheet.png` and `sheet.json` in code point order and the preview above.
`build:font` traces the sheet into `dist/FalseType.otf` and `.woff2`. To change a letter from the
canvas, edit `glyphs/sheet.png` directly at 1:1 and run `build:font` only.

## License

[SIL Open Font License 1.1](LICENSE). The letterforms are Wplace's canvas alphabet.
