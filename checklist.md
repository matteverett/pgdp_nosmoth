# Guiguts PP Process Checklist

"The genuine tryal of Dr. Nosmoth, a physican in Pekin, for the murder of the Mandarin Tonwin, treasurer to the army of the emperor of China, before the great council of Mandarines" by Anonymous

## Process the Pages
Our first set of activities will combine all proofed and formatted pages, fixing any errors and inconsistencies.

### Initial Setup
* Choose a short, simple project name, e.g. `pascal` for “*The Provincial Letters of Blaise Pascal*”
* Run the [setup script](https://github.com/tangledhelix/dp_pp_utils) to fetch the project resources and create the [Github](https://github.com/tangledhelix?tab=repositories&q=DP_&type=&language=&sort=) project
```shell
cd ~/dp/util
. venv/bin/activate
./make_project.py
```
* [X] Read the [project comments](https://www.pgdp.net/c/project.php?id=projectID676593ebf2d84#project-comments)
* [X] Subscribe to the [forum topic](https://www.pgdp.net/phpBB3/viewtopic.php?t=82933) and read all posts
* [X] Open `nosmoth-utf8.txt` in Guiguts
* [X] `File → Project → Configure Page Labels`. Check for roman numerals and unnumbered pages. Go to end of book to check page numbers line up.

### Sequential Inspection of Text
* [X] `Preferences → Appearance → Enable Scanno Highlighting`
* [X] Open images in Pixea: `open -a Pixea pngs`

Check for:

X Proper spacing for chapters and paragraphs
  X Before chapter start: 4 blank lines
  X Between chapter head and subhead: 1 blank line
  X Between head (or subhead) and chapter body: 2 blank lines
  X Pages should **not** start with a blank line unless starting a new chapter, section, or paragraph.
X Proper markup of `<i>italic</i>` and `<b>bold</b>`.
  X Watch for punctuation wrongly contained in markup, such as `<i>(ibid.</i>` or `<b>Subtopic.</b>`.
X Proper markup of Greek and other transliterations
X Languages other than the main book language can be noted for later
  X In HTML they can be labeled with `<span lang="fr">..</span>`
  X If they're in italic print, that's handled later during italic handling
X Block material all marked in some fashion:
  X Poetry, misc. tabular in `/* */`
  X Block quotes in `/# #/`
  X Where blocks cross page boundary, remove the extra markers around page marker
  X Each overall block should have blank lines before & after
X Join words hyphenated across page boundary
X Figures properly in `[Illustration: caption]`
  X Check that caption text agrees with List of Illustrations (if any)
  X Consistent spelling, abbreviation, capitalization in captions
  X For captionless (`[Illustration: ]`), remove colon & whitespace
X Fix Footnotes, Illustrations still inside a paragraph
  X Move outside paragraph to next or prior page, as appropriate
  X Don't worry about duplicate footnote numbers/symbols for now
  X Sidenotes are handled later
X Make notes of things that will need attention in the HTML:
  X Author cross-references like "`(p. 150)`" and "`see page 222`" that should become links.
  X How the editor laid out special sections such as tables and sidebars.
X Check that `[Blank Page]` are actually blank pages! Can also remove them.
X Note any illustrations in a list in `README.md` for later handling

* [X] Move illustrations to `illustrations/` folder

### Basic Fixup
* [X] Use `Tools → Basic Fixup` with all options checked.
     X Use it judiciously. E.g., you may want to turn off "Fix up spaces around hyphens" and "Format ellipses correctly."
* [X] `Tools → Remove End-of-line Spaces`
* [X] Remove any remaining `[Blank Page]` lines

### Errata
* [X] If original book had errata, apply it and note in TN

### Fix Block Markups and Proofer Notes
* [X] Use the `Search` menu to step through all `/* */` blocks.
     X Regex: `^(/\*|\*/)`
     X Check for a blank line before and after markup
     X Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
     X Close-up where broken at page boundaries, if not already done
     X Apply specific [indent value](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Table_Indent) if desired
     X Make sure poetry line numbers are at least two spaces to the right of the line.
* [X] Use the `Search` menu to step through all `/#..#/` blocks.
     X Regex: `^(/#|#/)`
     X Check for a blank line before and after markup
     X Make sure correct [Rewrap Markers](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Rewrap_Markers) are used
     X Close-up where broken at page boundaries, if not already done
     X Check consistent indentation of block text
     X Apply specific [margin values](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/Tools_Menu#Block_Quote_Indent_and_Margins) if desired
* [X] `Search → Find Next Proofer Comment`. Resolve all proofer's notes.
* [X] `Search → Find Orphaned DP Markup`.
* [X] Search `(</i>)([!?;:])` & replace `$2$1` to find punct that should move inside quotes
* [X] Use `Tools → Check Orphaned Brackets` to check each type of bracket and markup.
      X Do not omit the lowly parenthesis, often mis-scanned as curly-brace.
* [X] Look for malformed thought-breaks (5 stars). Regex: `\*\s*\*\s*\*\s*\*\s*\*`

### Format Front Matter
* [X] Format the title page, preserving as much of the original material as possible. Protect in `/X...X/` (no rewrap, no indent) or `/F...F/` (the same, except that it will be centered in the html version).
* [X] Edit the TOC. Find each matching chapter head; make sure heads are 1:1 with TOC. Protect TOC with `/X...X/`. Note that your TOC will probably need to be indented to prevent rewrapping, particularly if you use multiple spaces to align page numbers.
* [X] If book has illustrations, edit or create *List of Illustrations* (**Note:** this is not a requirement). Make sure it is 1:1 with `[Illustration]` captions. Protect with `/X...X/`.

### Edit Transliterations
* [X] Use `Tools → Character Tools` to search for transliterations. Check the content of each transliteration. For Greek, there's a "Greek Transliteration Tool", but entering Unicode Greek is preferable.

### Remove Visible Page Breaks
* [X] Run `Tools → Fixup Page Separators` to remove visible page separators

### Apply Word-Frequency Checks
* [X] Open `Tools → Word Frequency`. Double click on a word to search for it.
* [X] Set the `Frq` switch; click `All Words`. List is now sorted by word frequency; scroll to the end and skim up the list of words that only appear 1 time looking for oddities and obvious misspellings.
* [X] Click `Character Cnts`.
  X Note characters that appear only once, check usage.
  X Check for equal counts of left & right parens and brackets.
* [X] Set the `Alph` switch; click `All Words`. Scroll to the word Footnote and write down count for later use. (If the count is large, click once on Footnote and click 1st Harm. The harmonic window shows you any of the common misspellings of "Footnote" that occur.)
* [X] Click `Emdashes`. This shows words with emdashes in them as well as similar words without emdashes (aka: suspects) marked with `****`. Check suspects against the text and page images. Preserve author's intent even when inconsistent. **Hint**: Enable the `Suspects` flag and click `Emdashes` again to see only suspects words.
* [X] Click `Hyphens`. Same as Emdashes above but for Hyphens.
* [X] Click `Alpha/num`. Scan list for `one/ell` and `oh/zero` errors.
* [X] Click `ALL CAPS`. Scan list looking for oddities.
* [X] Click `MiXeD CasE`. Scan list looking for letters such as o that sometimes OCR wrongly as uppercase. `Oh/zero` errors can show up here, too.
* [X] Click `Check Accents`. Scan list looking for mistakes, inconsistent usages.
* [X] Click `Check , Upper`. Scan list for comma-for-period errors.
* [X] Click `Check . Lower`. Scan list for period-for-comma errors.
* [X] Click `Ital/Bold/SC`. Scan list for incorrect or inconsistent use of italics, bold face, and small caps.
* [X] Click `Ligatures`. Scan list for [incorrect or inconsistent use](https://www.pgdp.net/wiki/Æ_and_œ_ligatures) of `ae` and `oe` ligatures.
```text
æ Æ    <Opt> '    /ai/ to rhyme with “eye”.
œ Œ    <Opt> q    /ɔɪ/ to rhyme with “oi” in “foil”
<shift> for capital letter
```
* [X] Look for missed ligature / diacritical transliterations. Regex: `\[[^*]`

### Apply Scanno Checks
* [X] Use `Tools → Stealth Scannos` with `Auto Advance`.
  * [X] Start scanno searching based on `en-commn.rc`. Work through the list.
  * [ ] Apply scanno searching based on `misspelled.rc`. Work through the list.
  * [X] Apply scanno searching based on `regex.rc`. Work through the list.
* [X] `Tools → Run Jeebies`. Examine its report of possible `he/be` errors.

### Misc checks
* [X] Check for chapter/section spacing. Regex: `\n\n\n`
* [X] Check spaces around hyphens. Regex: `(\s+-|-\s+)`
* [X] Check spaces before punctuation. Regex: `\s+[.!?;:,]`
* [X] Check spaces around quotes. Regex: `(\s+['"][^\s]|[^\s]['"]\s+)`
* [X] Check spaces around brackets. Regex: `(\s+[({[\]})]|[({[\]})]\s+)`
* [X] Search regex `(Dr|M(me|lle|essrs|rs?)|St|Fr|Rev)\s` and add missing period if needed
* [X] Check `A.M.`, `P.M.` and similar for spacing to match book - regex: `[AP]\.\s*M\.`
  * Note these to do `&nbsp;` in HTML, to avoid line wrap mid-abbreviation
* [X] Does book use small-caps A.D. B.C.?
  * Search `[A-Z]\.\s*[A-Z]\.`, add `<sc>` and note for `&nbsp;` if needed
* [X] Check for multiple consecutive spaces which are not in a no-wrap block
* [X] Look at `<tb>` and look for improper uses
* [X] Check all ellipses. Regex: `\.\.\.`
* [X] Check for 3 dashes (not either 2 or 4). Regex: `[^-]---[^-]`
* [X] Look for spaces around em- or long-dash. Regex: `\s+--(--)?\s+`
* [X] Check adjacent letters and numbers. Regex: `([0-9][A-Za-z]|[A-Za-z][0-9])`
* [X] Superscripts (search `^` without regex). Can use `^` or `^{th}` form
  X Add TN to text version about this superscript notation

### Apply Bookloupe
* [ ] If you have Bookloupe installed, use `Tools → Bookloupe`.
  * Forward slash
  * HTML tag
  * No CR
  * Non-ASCII character
  * Non-ISO-8859 character
* Otherwise, use pptext from the [Post-Processing Workbench](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_Workbench).
* Work through the list, correcting as appropriate.

### Apply Spellcheck
* [X] Use `Tools → Spell Query`. Proceed through the document, correcting words or adding them to the project dictionary as appropriate.

### Fix Sidenotes
* [X] Read the [discussion](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Sidenotes). Step through sidenotes with: Search & Replace of `[S`, not regex, not whole word, ignore case. Click `Search` to find each Sidenote.
  * Compare to page image. Move note above paragraph if feasible.
  * Otherwise, position it above the sentence to which it applies, with blank lines to prevent rewrapping if you decide that is best.

### Fix Footnotes
* [X] Use `Tools → Footnote Fixup`. This will help you validate and move any footnotes.
  * `First Pass`
  * `Next / Prev FN` to navigate
  * Look for `*` and use `Join with Previous` to join them
  * THERE SHOULD BE NO ERRORS AT TOP OF WINDOW
    * Exception: sometimes a footnote is really long (brown)
    * Exception: multiple anchors per footnote can confuse it (teal)
* [X] Move footnotes between paragraphs
  * `Footnote Fixup`, `First Pass`
  * `All to Number`, `Reindex`
  * `First Pass`, `Move FNs to Para`
* [X] Save file, `Tools → Bookloupe` and check only `No punctuation at para end`
  * Run checks, find para and error, move footnotes as needed

### Fix Poetry Line Numbers
* [X] If the book has poetry that uses line numbers, read [this page](https://www.pgdp.net/wiki/PPTools/Guiguts/Fixup#Poetry_Line_Numbers) and align the line numbers consistently.

### Check balanced markup
Use the `Search` menu:

* [X] `Search → Find Orphaned Markup` (which searches for the regular expression `\<(\w+)>\n?[^<]+<(?!/\1>)`, that is any markup starting in `<..>` that doesn't end in an identical closing markup.
  * Note: this regular expression sees `<tb>` as unbalanced, and shows the text from the `<tb>` to the next markup as an error. (If you can devise a better regex please do!)
  * Possible alternate that explicitly lists all current markup `\<(i|b|sc|g||f|u)>\n?[^<]+<(?!/\1>)`
  * Because it includes a newline, the search may take several seconds to return the first result.
* [X] Correct the error and click search until no more are found.

### Consider page numbers and curly quotes
* [X] Curly quotes are [recommended](https://www.pgdp.net/phpBB3/viewtopic.php?f=3&t=73290) in both the text and HTML versions. Now is the time to put them in, before the split. Select `Txt → Convert to Curly Quotes`.
  * There are fixup menu items too
* [X] Search for remaining upright single quotation marks and replace them with either a ‘ or a ’.
* [X] Check for lingering straight quotes: `['"]`
* [X] `Txt → Curly Quote Corrections → Select Next @ Line` and handle each occurrence
* [X] Validate quotes pairings by searching for `[“”‘’]`

### Unicode dashes

* [X] Long dash: S/R `([^-])----([^-]|$)` → `$1——$2`
  * There exists a “long dash” Unicode character (TWO-EM DASH, U+2E3A). However, display support for it is not broad, so it’s better to use two consecutive EM DASH, which is widely supported.
* [X] Em dash: S/R `([^-])--([^-]|$)` → `$1—$2`
  * There exists another dash (HORIZONTAL BAR, U+2015) which one PM/PP prefers to EM DASH (using two bars for one EM DASH), based on appearance in text version. I opted not to use this in favor of using the EM DASH character in both text and HTML.
* [X] [En dash](https://www.pgdp.net/wiki/En-dash): S/R `([^-])-([^-]|$)` → `$1–$2`
  * Range of numbers `12–15`
  * Mathematical minus sign `15 – 12 = 3`
  * Negative numbers `–14º`
  * **Do not** use en-dash for fractions like `1-1/2` (or Convert Fractions function will be confused)
* Any dashes not covered above are simple hyphens.

### Last pre-split check
* [ ] Look at the revisit list for anything to handle before text/html split
* [X] Check for unexpected `*` to make sure no stray proofer notes or split-word/fn markers were missed

### Save Edited Markup
* [ ] Save any unsaved changes
* [ ] Use `File → Save a Copy As` to make `nosmoth.html`
  * This will be the starting file for the HTML version. You can also use it  as fallback in case you mess up and need to start the following steps over.

## Prepare the Plain Text Version
We now proceed to create a Plain Text Version of the book.

* [ ] Re-open `nosmoth-utf8.txt` (if not still open).

### Convert `<tb>`, Italic, Bold, and Smallcap
* [ ] Use `Txt → Txt Conversion Palette`:
  * [ ] Convert [inline formatting](https://www.pgdp.net/wiki/DP_Official_Documentation:Formatting/Formatting_Guidelines#Formatting_at_the_Character_Level:).
  * [ ] Convert [thought breaks](https://www.pgdp.net/wiki/DP_Official_Documentation:Formatting/Formatting_Guidelines#Thought_Breaks_.28Extra_Spacing.2FDecoration_Between_Paragraphs.29).
  * [ ] Convert [smallcaps](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Guide_to_smallcaps).

### Fix ASCII Tables
* [ ] Use `Search → Find Next /**/ Block` to step through all tabular material.
  * Compare to page image; reformat to best convey author intent.
  * For complex tables, try using `Txt → ASCII Table Effects` to reformat?
* [ ] Try this regex to validate that all border characters were replace with box drawing `[=+|-]`

### Rewrap and Clear Rewrap Markers
* [ ] Save the file if any unsaved changes.
* [ ] Use `Tools → Rewrap All`. Wait while rewrap completes.
* [ ] Page through entire text, looking for improper indentation. If found, re-open, clicking NO when asked if you want to save the edits. Find and fix broken rewrap markups. Repeat this step.
* [ ] Under `Tools → Footnote Fixup`, use the `Tidy Up Footnotes` button.
* [ ] Use `Tools → Clean Up Rewrap Markers`.
* [ ] Use `Tools → Remove End-of-line Spaces`.
* [ ] Rerun Bookloupe or pptext. Resolve any new issues.
* [ ] Save the document.

### Final checks
* [ ] Search for `<` and `>` to locate any tag markup not yet removed.

### Check revisit list
* [X] Check "things to revisit" list for anything lingering in the text version

### Add TN
* [X] Add transcriber's notes, example follows. Use 4+2 blank lines as in new chapter
* [X] Rewrap this section of text when finished.

```text
Transcriber’s Note


Some inconsistencies in spelling, hyphenation, and punctuation have been
retained.

This file uses _underscores_ to indicate italic text.
```

If bold is used, add also `and =equals= to indicate bold text`

If there were small-caps, `Small capitals changed to all capitals`

An example entry might look like this. Use the book's page numbers, not PNG number

```text
p. 123: changed “foo” to “fool” (the fool and his money)
```

### Final review
* [ ] Skim over text file to find any obvious issues

### Validation
* [ ] Run [PWBB](https://www.pgdp.net/ppwb/index.php) pptext check
* [ ] Run text checks at [pptools](https://pptools.tangledhelix.com)

## Prepare the HTML Version
Finally, we create an HTML version of the book.

### Generate the HTML
* [ ] Open `nosmoth.html` that was saved previously.
* [ ] It is preferable for the source line-breaks to match the book; however HTML poetry markup won't work unless `/P..P/` sections have been rewrapped. If the book has much poetry, rewrap it all; else select and rewrap poetry sections individually.
  * Don't remove the rewrap markers. These are needed for generation of proper HTML.
* [ ] Open `HTML → HTML Generator`.
  * Set optional switches as desired.
  * Use the `Autogenerate HTML` button.
* [ ] Save the file and open it in a browser by using the `View in Browser` button.
* [ ] Scroll through looking for systematic errors. (Title pages, tables, etc. will look terrible; no matter). If automatic conversion messed up, start this step over with a reset file.
* [ ] Page through the book looking for text that was not handled well by automatic HTML generation, in particular:
  * [Title pages](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Title_Pages).
  * [Tables and Tables of Contents](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Tables). The `Auto Table` button can help format tables.
    * A book with wide tables that don't render well may benefit from the page numbers moving to the left margin. This is easy to do, just change `left` under the `.pagenum` class to something like `2%` or `1.5%`. I used `1.5%` for `presidents`.
  * [Indexes](https://www.pgdp.net/wiki/Indexes) - can use Guiguts feature but if it formats poorly, see link for a different method.
    * [ ] Sanity-check index for links, improper line breaks, etc.
    * [ ] Review index for "see X" entries and link any of those manually
  * Illustrations.
* [ ] Use `HTML → HTML Markup` to make improvements. Use regex replacements to make systematic changes.
  * Where you see a problem, make a correction in Guiguts, save the file, and click the "reload" button in the web browser.
* [ ] Hyperlink page references in text, TOC, and index (discussed [here](https://www.pgdp.net/wiki/PPTools/Guiguts/HTML#Hyperlinking_Page_Numbers) and [here](https://www.pgdp.net/wiki/Indexes)).
* [ ] Remove the [Generated TOC](https://www.pgdp.net/wiki/PPTools/Guiguts/Guiguts_Manual/HTML_Menu#Generated_TOC) if it is not needed.
* [ ] If `A.M.` `P.M.` or similar abbreviations were used and have spaces, insert `&nbsp;` to avoid undesirable mid-abbreviation line wraps.
* [ ] If superscripts were used, convert to `<sup>`
* [ ] Semantic fixup for italics
  * Search `<i>((.|\n)+?)</i>`
  * Replace (emphasis) `<em>$1</em>`
  * Replace (citation) `<cite>$1</cite>`
  * Replace ([languages](http://www.w3schools.com/tags/ref_language_codes.asp)) `<i lang="fr">$1</i>`
  * Leave other cases as `<i>..</i>`
* [ ] Add `abbr` tags if appropriate. ([Reference](https://www.pgdp.net/wiki/Accessibility_Recipes/Abbreviations))
* [ ] If there is a cover image for e-readers supplied with the project, or you are creating one yourself, you can find information on what is needed in your HTML in the [Proofreaders' Guide to EPUB](https://www.pgdp.net/wiki/The_Proofreader%27s_Guide_to_EPUB#Cover_Page) or the [PP guide to cover pages](https://www.pgdp.net/wiki/PP_guide_to_cover_pages).

### Fractions
For consistency the superscript/subscript form of fractions might be best (e.g. the 3-character ¹⁄₂ vs. single-character ½). A few fractions have a single character form but most do not. And fractions like 5/16 have no 3-char form even, you need 4 ...

This regex: `([¹²³⁴⁵⁶⁷⁸⁹⁰]+⁄[₁₂₃₄₅₆₇₈₉₀]+)` may be of use to locate fractions once converted.

### Process Hi-resolution Images
If the project manager provided high-resolution scans of the images in the text, use an image processing program such as GIMP or Adobe Photoshop Elements to optimize them—see [Guide to Image Processing](https://www.pgdp.net/wiki/Guide_to_Image_Processing). You can do this before, during, or after HTML conversion.

Unless purely decorative, add an `alt` tag for each image unless it has a caption. For decoration, use `alt="" data-role="presentation"` (empty string to satisfy the validator).

Taken from a [forum post](https://www.pgdp.net/phpBB3/viewtopic.php?p=1354798&sid=db2ca383a2ce4e9d70bc598253bb0936#p1354798):
> DO
> - use an empty string for purely decorative images.
> - when an image is meant to convey an action, try to use a single word: download" or "email".
> - be concise.
> - remember that the purpose of a cover image is to intrigue a reader.
> - use the language of the text for the alt-text
> - think about what an image is meant to convey
>
> DON'T
> - use text like "image" or "figure 22" in alt-text. That's just taunting a blind reader.
> - use the file name for alt text.
> - repeat what is already in a caption.
> - describe details that are irrelevant to the narrative.
> - describe logos. Just identify them.
> - make up shit.

Image [sizes](https://www.pgdp.net/phpBB3/viewtopic.php?f=3&t=70286):
* Inline: up to 256K, 5000x5000 pixels
* Linked: up to 1MB, 5000x5000 pixels. Should only need linked images for large or complex things, e.g. maps.
* Covers: see [cover documentation](https://www.pgdp.net/wiki/PP_guide_to_cover_pages). Recommend 1600x2560, aspect ratio ~1:1.6. Not over 5000x5000px. Minimum 650x1000. **No specific file size limit**, but use judgement and don't make it larger than necessary.

For each image:
* [ ] Load image from the `illustrations/` folder (see the Initial Setup step).
* [ ] Straighten it (almost all scanned images are off-perpendicular; some are trapezoidal owing to the page not being flat on the scan window). Perspective tool.
* [ ] Crop it to remove all redundant white space and borders (provide margins and borders with CSS styling of the `<img>` markup).
* [ ] Correct the contrast
* [ ] Use the [dodge/burn layer technique](https://www.pgdp.net/wiki/Guide_to_Image_Processing#Linear_Light_in_The_GIMP) to clean up, at least for line drawings
* [ ] Sharpen.
* [ ] Correct any major scratches, freckles, dirt, etc.
* [ ] Save in the subfolder images using appropriate type:
  * Line drawings in `.png` at 8 bits per pixel (not the default 24-bit RGB format).
  * Photographs as `.jpg` with an appropriate compression level such as (Photoshop) level 6.
* [ ] Under `HTML → HTML Generator`, use the `Auto Illus Search` button. This will help add the images to the book.
* [ ] Page through entire HTML book making sure that each image is being loaded correctly. Test each thumbnail if used.
* [ ] If any images were modified substantially (including removing a library sticker or stamp), add a TN. Place the new image in the public domain in the TN. This is a PG requirement.
* [ ] If fabricating your own cover, add the TN as noted in [Easy_Epub/Cover](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Easy_Epub/Cover).

### Check "things to revisit"
* [ ] Check revisit list for anything left for the HTML version

### Add TN
* [ ] Add transcriber's notes, example follows.

```html
<div class="transnote">
<h2>Transcriber’s Note</h2>

<p>
Some inconsistencies in spelling, hyphenation, and punctuation have been
retained.
</p>
</div>
```

An example entry might look like this. Use the book's page numbers, not PNG number.

```html
<ul>
<li>
<a href="#Page_123">p. 123</a>: changed “foo” to “fool”
(<a href="#TN1">the fool and his money</a>)
</li>
</ul>
```

And accompany this with a target in the correction site, e.g. the below.
Use a `<span>` if another element isn't already present; otherwise use the
existing element and add the `id` attribute.

```html
They say that <span id="TN1">the fool and his money</span> are soon separated
```

* [ ] Make sure the TN has no straight-quotes `'"` and instead uses curly quotes `“”‘’`

### Validate HTML and CSS
Perform these validation steps before submitting your book. Validation is also helpful while customizing the HTML and CSS above.

* [ ] File should start with HTML opening
```html
<!DOCTYPE html>
<html lang="en">
```
* [ ] Confirm that the `<title>` tag matches the format specified by the [Post-Processing FAQ](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Post-Processing_FAQ#HTML_title).
  * `<title>Alice's Adventures in Wonderland | Project Gutenberg</title>`
  * Sentence case isn't required here (but it is on the upload form)
* [ ] Use `HTML → HTML Tidy`. Fix any reported problems.
* [ ] Use [W3C Markup Validation Service](http://validator.w3.org/#validate-by-upload). Fix any reported problems.
* [ ] Remove unused CSS. `HTML → PPhtml` can help with this. Alternatively, check manually or use a tool such as the Firefox addons Firebug (with CSS Usage extension) or Dust-Me Selectors.
* [ ] Use [W3C CSS Validation Service](http://jigsaw.w3.org/css-validator/#validate_by_upload). Fix any reported problems.
  * Validate as CSS 2.1
  * CSS3 is acceptable if current status is `REC` on [this page](https://www.w3.org/Style/CSS/current-work)
    * e.g. CSS3 drop-caps
    * or use of `display: flex;` for centering a div (poetry)
    * if uploading CSS3, leave a note for WWer about it.
* [ ] Use `HTML → HTML Link Checker`. Fix any reported problems.
* [ ] Use `HTML → PPVimage` to check for image-related errors. Fix any reported problems.
* [ ] Run [PWBB](https://www.pgdp.net/ppwb/index.php) checks
  * [ ] [pphtml](https://www.pgdp.net/ppwb/pphtml.php)
  * [ ] [ppcomp](https://www.pgdp.net/ppwb/ppcomp.php) to compare text/html files
* TODO: add pptools here when it supports HTML5
  * CSS transform for pptools:
```css
/* projects with bold <b> markup */
b:before { content: "="; }
b:after { content: "="; }
```

### Review HTML
* [ ] Review in multiple browsers (Safari, Chrome, Firefox, maybe Edge?)
* [ ] Pay particular attention to complex items like tables, poetry

## Ebook generation

### Notes on rendering
#### CSS
* Don't use `!important`, ADE has a parsing issue with it (probably others do too)
* ADE doesn't render small-caps
* Kindle doesn't seem to honor `width` on divs? Set all of `min-width`, `width`, `max-width` to fix. Kindle may set `min-width` 100% and need an override?
  * Other advice: "Kindle ignores max-width. If you want your narrow text to be centered (column-centered with smooth margins), add `margin: auto;` to the "narrow" definition. Otherwise, it'll be left-positioned along the body's main left margin.
* Kindle doesn't always honor `page-break-*` CSS
* Moon+ mis-handles drop-cap images; it should ignore them but doesn't. A DP user reported this bug so it may be fixed in the future.
    * Moon+ has many other rendering issues too -- I no longer do previews in it for that reason.

#### Tables
* E-readers are bad at wide tables and non-trivial tables
* Nook is particularly bad at table rendering
* Apple Books isn't reliably able to show PNGs in table cells??

#### Images
* Kindle on Mac renderes PNG transparent backgrounds as black
* If no cover was included, the first illustration is used instead.
* Kindle sometimes can show SVG, sometimes not??

#### General rendering
* Sometimes page breaks show in weird places due to ebookmaker's chunking
* Renaming epub3 to end in `.kepub.epub` improves rendering a lot
* Also a utility `kepubify` (link below) that converts; it's unclear what this conversion does that's any better than just renaming the file. Changing the filename is enough to invoke a different / better rendering engine on Kobo devices.

### Build and upload Ebooks
* [X] `make zip`
* [X] Upload to [ebookmaker](https://ebookmaker.pglaf.org/) to generate Ebook files
* [X] `make ebooksget cache={cache_number}` to download ebook files
* [X] Convert epub3 with [kepubify](https://pgaskin.net/kepubify/try/)
* [X] Upload epub3 with [Send to Kindle](https://www.amazon.com/gp/sendtokindle)
* [X] Add epub3 to Apple Books
* [ ] Add epub, epub3, renamed-kepub, converted-kepub to Dropbox for Kobo

### Ebook review
<details>
<summary>
Don't necessarily have to do *all* of these, but these are what I have.
</summary>

* [ ] Review Ebook ToC in at least one e-reader, for structure & content
  * Can try using `title=` attr if a header title has footnote marker etc.
* [ ] Mac
  * [ ] Adobe Digital Editions (epub3)
  * [ ] Apple Books
  * [ ] Kindle Previewer (epub3)
  * [ ] Calibre (epub3)
* [ ] Phone
  * [ ] Apple Books (iPhone)
  * [ ] Kindle (iPhone)
* [ ] Tablet
  * [ ] Kindle (Android)
  * [ ] Google Play Books - Android (Dropbox)
  * [ ] Apple Books - iPad mini
* [ ] E-ink
  * [ ] Kobo Libra Colour (renamed-kepub)
  * [ ] Kobo Libra Colour (converted-kepub)
  * [ ] Kindle Paperwhite

</details>

## Smooth Reading

### Submit to SR pool

Submit for a decent length of time, up to the maximum. Check what's in `ebooks/` folder, it'll all be uploaded.

* [X] Make sure git is clean, committed, pushed
* [X] `make sr`
* [X] Go to [project page](https://www.pgdp.net/c/project.php?id=projectID676593ebf2d84), select SR time period, upload `nosmoth-sr.zip`
* [X] Subscribe to “user uploads a SR report” item
* [X] Update my Trello project board with due date, set card to SR status
* [X] If time permits, smooth read it myself as well

### Process SR feedback
* [ ] After SR is finished, processed SR feedback into project.
* [ ] Add **anonymized** files to git, e.g. `nosmoth-smoothread01.txt`
* [ ] Thank your smooth readers with a PM!
* [ ] If there were changes from the SR round, re-do final checks from above (validators etc)

## Upload the Finished Project

[Guide to DU and Posting to PG](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/Guide_to_Direct_Uploading_%28DU%29_and_Posting_to_PG)

* [ ] Run through [ebookmaker](https://ebookmaker.pglaf.org/), check output.txt
  * No errors!
  * Warnings are OK
  * Copy link to the output.txt file (will persist about 3 days)
* [ ] `make zip`
* [ ] Go to the [PGLAF upload site](https://upload.pglaf.org/)
* [ ] Enter copyright clearance (get from DP [project page](https://www.pgdp.net/c/project.php?id=projectID676593ebf2d84))
* [ ] Choose zip file to upload
* [ ] Add `dp-post@pgdp.net` as a Cc on Posted announcement
* [ ] Carefully check submission details against title page from book
  * If anything won't fit in the form add it to the Notes field
  * If you make any changes mention them in Notes field
  * Use sentence case for title. Proper nouns such as names should be capitalized.
    * The story of the little red hen
    * What the wind did
    * The writing of fiction
    * Travels in Africa, Egypt, and Syria from the year 1792 to 1798
    * The Squire's young folk : A Christmas story
* [ ] Credits line
  * Paste in from DP [project page](https://www.pgdp.net/c/project.php?id=projectID676593ebf2d84)
  * Add myself to credits line
  * DO NOT alter any other names, DO NOT turn a DP username into real name!
  * Assume `Produced by` will be added as a prefix to whatever you enter
  * Should be only ASCII, no Unicode
  * Example: `Joe Schmo, Jane Doe, and the Online Distributed Proofreading Team at https://www.pgdp.net (This file was produced from images generously made available by The Internet Archive/American Libraries.)`
* [ ] Anything else important, add to Notes field
  * Any CSS3 should be noted, e.g. drop-cap or other stuff.
  * If project contains Hebrew, let WWer know that
* [ ] Preview the submission
  * **After preview you have to select the upload file again!**
  * [ ] If the preview looks good and indicates no problem, then submit
* If you notice an error post-upload, contact pgww at lists.pglaf.org ASAP
* If you notice an error in your own recently posted project, contact pgww at lists.pglaf.org ASAP
* For projects over a month old, use the [errata process](https://www.gutenberg.org/help/errata.html)
* If not posted within a week, contact WWers pgww at lists.pglaf.org

## Project wrap-up
* [ ] When posted, then update PG URL in README.md, and [personal website list](https://tangledhelix.com/about), and set homepage on GitHub project

### Device / cloud cleanup
* [ ] Remove from Dropbox
* [ ] Remove from Kindle and Kindle library
* [ ] Remove from Apple Books
* [ ] Remove from Kobo device

## Related Pages
* [Beginner PP advice](https://www.pgdp.net/wiki/Beginner_PP_advice)
* [Post-Processing FAQ](https://www.pgdp.net/c/faq/post_proof.php)
* [Post-Processing Advice](https://www.pgdp.net/wiki/Post-Processing_Advice)
* [Guiguts Tutorial](https://www.pgdp.net/wiki/Guiguts_Tutorial)
* [Guiguts Manual](https://www.pgdp.net/wiki/PPTools/Guiguts)
* [Getting your PP Project Ready for PPV](https://www.pgdp.net/wiki/Getting_your_PP_Project_Ready_for_PPV)
* [Poetry Case Study](https://www.pgdp.net/wiki/DP_Official_Documentation:PP_and_PPV/DP_HTML_Best_Practices/Case_Studies/Poetry)