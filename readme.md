# wavefont

A typeface for rendering data: waveforms, spectrums, diagrams, bars etc. [Demo](https://a-vis.github.io/wavefont).

<a href="https://a-vis.github.io/wavefont"><img src="./preview.png" width="240px"/></a>

Font provides bar glyphs representing values from 0 to 100 (and clipping 28 values) for data.

The data charcodes fall under _Latin Extended-A_ unicode category (U+0100-017F), therefore recognized as word boundary in regexps, can be selected by <kbd>Ctrl</kbd> + <kbd>→</kbd> or double click.

Vertical position of a bar can be adjusted via combining accent grave <kbd>&nbsp;&#x0300;</kbd> (U+0300) for negative shift or via accent acute <kbd>&nbsp;&#x0301;</kbd> (U+0301) for positive shift. One accent character adjusts vertical position by _1_. To provide shift by more than 1 - use multiple accents in a row. Note that using accents introduces editing side effect - cutting a fragment with accents shifts baseline outside the fragment. To compensate that, use `oncut`/`onpaste` events.

Font provides variable features:

Tag | Range | Meaning
---|---|---
`wdth` | _1_-_100_ | Adjusts glyph width.
`algn` | _0_-_1_ | _0_ for bottom align, _0.5_ for center and _1_ for top align.
`radi` | _0_-_50_ | Border radius, percentage of glyph width.

## Usage

Get [otf](./font/wavefont.otf) or [ttf](./font/wavefont.ttf) font.

```html
<style>
	@font-face {
		font-family: "wavefont";
		font-weight: normal;
		src: url("./wavefont.otf");
		font-display: block;
	}
	.wavefont {
		font-style: wavefont;
		--wdth: 10;
		font-variation-settings: 'wdth' var(--wdth), 'algn' 0.5, 'radi' 30;
	}
</style>

<textarea id="waveform" class="wavefont" cols="100">
	&#x0100;&#x0101;&#x0102;&#x0103;&#x0301;&#x0104;&#x0105; ... &#x017f;
</textarea>

<script>
	// transform numbers from 0..100 range to characters 
	wavefotm.textContent = data.map(value => String.fromCharCode(0x100 + value))
</script>
```

## Building

UFOs are generated by [plop](https://github.com/plopjs/plop), to modify font the [plopfile](./plopfile.js) change is required.
TTF is built with [fontmake](https://github.com/googlefonts/fontmake). OTF is built with [afdko](https://adobe-type-tools.github.io/afdko/).

## See also

* [linefont](https://github.com/a-vis/linefont)

## References

* [unified font object spec](https://unifiedfontobject.org/versions/ufo3) − unified human-readable format for storing font data.
* [feature file spec](https://adobe-type-tools.github.io/afdko/OpenTypeFeatureFileSpecification.html#6.h) − defining opentype font features.
* [afdko](https://adobe-type-tools.github.io/afdko/) − font building tools from Adobe.
* [fontmake](https://github.com/googlefonts/fontmake) − font building tool from Google.
* [unicode-table](https://unicode-table.com/) − convenient unicode table.
* [adobe-variable-font-prototype](https://github.com/adobe-fonts/adobe-variable-font-prototype) − example variable font.
* [designspace xml spec](https://github.com/fonttools/fonttools/tree/main/Doc/source/designspaceLib#document-xml-structure) − human-readable format for describing variable fonts.
* [plopfile](https://github.com/plopjs/plop#built-in-actions) − file generator based on templates.

<p align="center">🕉<p>
