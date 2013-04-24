# Principles of Writing Consistent, Idiomatic CSS

The following document outlines a reasonable style guide for CSS development.
These guidelines strongly encourage the use of existing, common, sensible
patterns. They should be adapted as needed to create your own style guide.

This is a living document and new ideas are always welcome. Please contribute.


## Table of Contents

1. [General Principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [Format](#format)
5. [Declaration Order](#declaration-order)
6. [Practical Example](#example)
7. [Afterword](#afterword)

[Acknowledgements](#acknowledgements) & [License](#license).


<a name="general-principles"></a>
## 1. General Principles

<blockquote>
“Part of being a good steward to a successful project is realizing that writing
code for yourself is a bad idea. If thousands of people are using your code,
then write your code for maximum clarity, not your personal preference of how
to get clever within the spec.”
<br />
— <b>Idan Gazit</b>.
</blockquote>

<blockquote>
“Arguments over style are pointless. There should be a style guide, and you
should follow it.”
<br />
— <b>Rebecca Murphey</b>.
</blockquote>

<blockquote>
“The only programming project with no disagreement whatsoever on code
formatting is the one you work on alone.”
<br />
— <b>Jeff Atwood</b>.
</blockquote>

* You are not a human code compiler/compressor, so don’t try to be one.
* All code in any code-base should look like a single person typed it, no
  matter how many people contributed.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style, use existing, common patterns.


<a name="whitespace"></a>
## 2. Whitespace

Only one style should exist across the entire source of your code-base. Always
be consistent in your use of whitespace. Use whitespace to improve readability.

* _Never_ mix spaces and tabs for indentation.
* Choose between soft indents —spaces— or real tabs. Stick to your choice
  without fail. _Preference: spaces_.
* If using spaces, choose the number of characters used per indentation level.
  _Preference: 2 spaces_.

Tip: configure your editor to “show invisibles”. This will allow you to
eliminate trailing whitespace, eliminate unintended blank line whitespace,
and avoid polluting diffs.


<a name="comments"></a>
## 3. Comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don’t leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code-base.

* Place comments on a new line above their subject.
* Make liberal use of comments to break CSS code into discrete sections.
* Use “sentence case” style in single-line, multi-line and tag comments.

Sections comments:

```css
/* ======================================================================
   > 1st Section Title
   ====================================================================== */

/* ============================================================
   >> 2nd Section Title
   ============================================================ */

/* --------------------------------------------------
   >>> 3rd Section Title
   -------------------------------------------------- */

/* ----------------------------------------
   >>>> 4th Section Title
   ---------------------------------------- */
```

Single-line and multi-line comments:

```css
/* The first sentence of the multi-line comment starts here and continues on
 * this line for a while finally concluding here at the end of this paragraph.
 *
 * The multi-line comment is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 */

/* This is a single-line comment. */
```

Tags:

```css
/* TODO: flag something to be completed at a later date. */
/* FIXME: flag something that is bogus and broken. */
/* BEWARE: flag something that is bogus but works. BEWARE AKA XXX. */
/* TEST: flag something that is being tested. */
```

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.


<a name="format"></a>
## 4. Format

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include single space after the colon of a declaration.
* Use lowercase and shorthand hex values _when possible_ —e.g. `#fff` rather
  than `color: #ffffff`—.
* Use single or double quotes consistently. _Preference: single quotes_.
* Quote attribute values in selectors —e.g. `input[type='checkbox']`—.
* Quote URL values —e.g. `url('images/foobar.png')`—.
* _Where allowed_, avoid specifying units for zero-values —e.g. `margin: 0`
  rather than `margin: 0em`—.
* _Where allowed_, simplify non-integer values —e.g. `margin: .5em` rather
  than `margin: 0.5em`—.
* Include a space after each comma in comma-separated property or function
  values.
* Include a semi-colon at the end of the last declaration in a declaration
  block.
* Place the closing brace of a ruleset in the same column as the first
  character of the ruleset.
* Separate each ruleset by a blank line.

Example:

```css
.selector-1,
.selector-2,
.selector-3[type='text'] {
  display: block;
  font-family: helvetica, arial, sans-serif;
  color: #333;
  background: #fff;
  background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}

.selector-a {
  padding: .5em;
  background: url('images/foobar.png');
}
```

### 4.1 Exceptions and Slight Deviations

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

Example:

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values —such as collections of gradients or
shadows— can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs. There are two formats that could
be used.

Example:

```css
.selector {
  box-shadow: 1px 1px 1px #333,
    2px 2px 1px 1px #ccc inset;
  background-image:
    linear-gradient(#fff, #ccc),
    linear-gradient(#f3c, #4ec);
}
```

### 4.2 Preprocessors: Additional Format Considerations

Different CSS preprocessors have different features, functionality, and syntax.
Your conventions should be extended to accommodate the particularities of any
preprocessor in use. The following guidelines are in reference to Sass.

* Limit nesting to 1 level deep —or 2 if you are targeting a pseudo-class or
  a pseudo-element with “&”—. Reassess any nesting more than 2 levels deep.
  This prevents overly specific CSS selectors.
* Avoid large numbers of nested rules. Break them up when readability starts to
  be affected.
* Always place `@extend` statements on the first lines of a declaration
  block.
* Where possible, group `@include` statements at the top of a declaration
  block, after any `@extend` statements.
* _Consider_ prefixing custom functions with `x-` or another namespace. This
  helps to avoid any potential to confuse your function with a native CSS
  function, or to clash with functions from libraries.

Example:

```scss
.selector-1 {
  @extend .other-rule;
  @include clearfix();
  @include box-sizing(border-box);
  width: x-grid-unit(1);
  // Other declarations.
}
```


<a name="declaration-order"></a>
## 5. Declaration Order

Declarations should be ordered in accordance with a single principle.
There are three main ways: alphabetical, grouped by type or by length.
The preference is to group by type. Here is offered a list of preference order,
but you could do it in a more simpler way, declaring structurally important
properties —e.g. positioning and box-model— prior to all others.

Note that in the bellow list, are only listed the short-hand declarations or
just a name pattern followed by “-*”. The following declarations can be placed
in any order, nevertheless, be consistent.

1. Generated content: `content`, `counter-*` and `quotes`.
2. Dimensions, padding, margin and box display: `width`, `height`, `min-*`,
   `max-*`, `padding-*`, `margin-*`, `box-sizing`, `display`, `visibility`,
   `clip`, `overflow-*` and `z-index`.
3. Position, float and vertical align: `position`, `top`, `right`, `bottom`,
   `left`, `float`, `clear` and `vertical-align`.
4. Lists and table: `list-*`, `border-collapse`, `border-spacing`,
   `caption-side`, `empty-cells` and `table-layout`.
5. User interface: `appearance`, `box-shadow`, `resize`, `cursor` and `opacity`.
6. Typography: `font-*`, `text-*`, `letter-spacing`, `line-height`,
   `white-space`, `word-*`, `direction` and `color`.
7. Animations, transformations and transitions: `animation-*`, `transform-*`,
   `perspective-*`, `backface-visibility` and `transition-*`.
8. Background, border and outline: `background-*`, `border-*` and `outline-*`.
9. Vendor prefixes: `-webkit-*`, `-moz-*`, `-ms-*` and `-o-*`.

Example:

```css
.selector {
  width: 75%;
  height: 50%;
  padding: 1em;
  margin: 0 0 2em;
  box-sizing: border-box;
  display: inline-block;
  overflow: hidden;
  z-index: 10;
  position: relative;
  top: 1em;
  left: 2em;
  font-family: sans-serif;
  font-size: 12em;
  text-align: right;
  color: #fff;
  background: #333;
  border: .2em solid #111;
}
```

Strict alphabetical ordering or bye length are also relatively popular, but the
drawback is that separates related properties. For example, position offsets
are no longer grouped together and box-model properties can end up spread
throughout a declaration block.


<a name="example"></a>
## 6. Practical Example

An example of various conventions.

```css

/* ======================================================================
   > Grid Layout
   ====================================================================== */

/* Column layout with horizontal scroll.
 *
 * This creates a single row of full-height, non-wrapping columns that can
 * be browsed horizontally within their parent.
 *
 * Example HTML:
 *
 * <div class="grid">
 *   <div class="cell cell-3"></div>
 *   <div class="cell cell-3"></div>
 *   <div class="cell cell-3"></div>
 * </div>
 */

/* Grid container.
 * Must only contain `.cell` children.
 */

.grid {
  height: 100%;
  /* Remove inter-cell whitespace. */
  font-size: 0;
  /* Prevent inline-block cells wrapping. */
  white-space: nowrap;
}

/* Grid cells.
 * No explicit width by default. Extend with `.cell-n` classes.
 */

.cell {
  height: 100%;
  /* Set the inter-cell spacing. */
  padding: 0 10em;
  box-sizing: border-box;
  display: inline-block;
  overflow: hidden;
  position: relative;
  vertical-align: top;
  /* Reset font-size. */
  font-size: 16em;
  /* Reset white-space. */
  white-space: normal;
  border: .2em solid #333;
}

/* Cell states. */

.cell.is-animating {
  background-color: #fffdec;
}

/* ============================================================
   >> Cell Dimensions
   ============================================================ */

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }

/* ============================================================
   >> Cell Modifiers
   ============================================================ */

.cell--detail,
.cell--important {
  border-width: .4em;
}
```


<a name="afterword"></a>
## 7. Afterword

It doesn’t actually matter which code style is used in a code-base. What
really does matter is that everyone on the team sticks with those conventions
and uses them consistently.

So, if you’re editing code, take a closer look and determine its style. If
spaces are being used for indentation, use spaces; if single quotes are being
used for any given purpose, use single quotes too. Bottom line, do what is
being done. Period.

The whole point of having a style guide is to have a common vocabulary, so
people can concentrate on what you’re saying rather than on how you’re saying
it. If code you add to a file looks drastically different from the existing
code around it, it throws readers out of their rhythm when they go to read it.
Avoid this. __Be consistent__.


<a name="acknowledgements"></a>
## Acknowledgements

Based on [Idiomatic CSS](//github.com/necolas/idiomatic-css).
Inspired on [Idiomatic JavaScript](//github.com/rwldrn/idiomatic.js),
[Google HTML/CSS Style Guide](//google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) &
many others.


<a name="license"></a>
## License

_Principles of Writing Consistent, Idiomatic CSS_ is licensed under
[Creative Commons](//creativecommons.org/licenses/by/3.0/).
This applies to all documents in this repository.