# FalseType

yet another pixel-perfect font. pun on truetype cause it's not anti-aliased.

## Use

Copy `dist/FalseType.woff2` into your site.

```css
@font-face {
  font-family: 'FalseType';
  src: url('/fonts/FalseType.woff2') format('woff2');
  font-weight: 100 900;
  font-display: block;
}

.thing {
  font-family: 'FalseType', monospace;
  font-size: 1.5rem;
  line-height: 1;
  letter-spacing: 0;
  font-kerning: none;
  font-synthesis: none;
}
```

Sizes that stay on the pixel grid are multiples of 12px: 0.75rem, 1.5rem, 2.25rem, 3rem. Anything else blurs, and so does browser zoom other than 100%.

There is one weight and no italic. `font-synthesis: none` stops the browser faking them.

Caps are 8 pixels, x-height 5, descenders 3. The em is 12 pixels with the baseline 10 down, so at `line-height: 1` the baseline lands where Arial's or Archivo's does at the same size.

## Build

```sh
npm install
npm run build
```

`build:sheet` turns `glyphs/extra-glyphs.mjs` plus the letters in `glyphs/sheet.png` into a sheet in code point order, and writes `glyphs/charset-preview@8x.png`. `build:font` traces the sheet into `dist/FalseType.otf` and `dist/FalseType.woff2`.

## Edit

- Letters: edit `glyphs/sheet.png` at 1:1, then `npm run build:font`.
- Everything else: `glyphs/extra-glyphs.mjs`. `EXTRA_GLYPHS` are bitmaps, rows top to bottom in an 11 row frame from the cap top, `#` for ink. `COMPOSED` builds accented letters from a base letter and a mark in `MARKS`. A bitmap in `EXTRA_GLYPHS` wins over a composed one. Then `npm run build`.
- Check `glyphs/charset-preview@8x.png` before you commit.

## Charset

Printable ASCII, Latin-1 letters plus Œ œ Š š Ž ž Č č Ÿ, curly quotes and dashes, `€ £ ¥ ¢`, arrows, checks, stars, hearts. No kerning yet.

## License

[OFL 1.1](LICENSE).
