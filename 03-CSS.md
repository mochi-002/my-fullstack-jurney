# CSS — Complete Study Notes

> **CSS (Cascading Style Sheets)** is the language used to style and visually present HTML elements on a webpage. "Cascading" means styles flow from top to bottom, and more specific rules override general ones.

---

## Table of Contents

1. [Syntax](#syntax)
2. [Selectors](#selectors)
3. [Adding CSS to HTML](#adding-css-to-html)
4. [The Cascade & Specificity](#the-cascade--specificity)
5. [Colors](#colors)
6. [Background](#background)
7. [Box Model](#box-model)
8. [Display](#display)
9. [Visibility](#visibility)
10. [Dimensions](#dimensions)
11. [Overflow](#overflow)
12. [Text & Typography](#text--typography)
13. [Inheritance](#inheritance)
14. [Mouse Cursor](#mouse-cursor)
15. [Float & Clear](#float--clear)
16. [CSS calc()](#css-calc)
17. [Opacity](#opacity)
18. [Position](#position)
19. [Z-index](#z-index)
20. [Lists & Tables](#lists--tables)
21. [Pseudo-Classes](#pseudo-classes)
22. [Pseudo-Elements](#pseudo-elements)
23. [Vendor Prefixes](#vendor-prefixes)
24. [Border Radius](#border-radius)
25. [Box Shadow](#box-shadow)
26. [Box Sizing](#box-sizing)
27. [Grouping & Nesting Selectors](#grouping--nesting-selectors)

---

## Syntax

Every CSS rule follows the same structure:

```css
selector {
  property: value;
}
```

- **Selector** — targets the HTML element(s) you want to style.
- **Property** — the style attribute you want to change (e.g., `color`, `font-size`).
- **Value** — what you set the property to.

```css
/* Example */
h1 {
  color: navy;
  font-size: 32px;
}
```

---

## Selectors

Selectors tell CSS which elements to style.

```css
/* Universal — targets ALL elements */
* {
  margin: 0;
  padding: 0;
}

/* Element selector — targets all <p> tags */
p {
  color: gray;
}

/* Class selector — targets elements with class="btn" */
.btn {
  background-color: blue;
}

/* ID selector — targets the element with id="header" */
#header {
  background-color: black;
}
```

> **Best Practice:** Prefer **classes** (`.class`) over IDs (`#id`) for styling. IDs have very high specificity and are harder to override. Reserve IDs for JavaScript hooks.

---

## Adding CSS to HTML

There are three ways to apply CSS. They differ in **scope** and **specificity**.

### External Stylesheet _(Recommended)_

A separate `.css` file linked in the `<head>`. Best for maintainability.

```html
<link rel="stylesheet" href="css/master.css" />
```

### Internal Style

CSS written inside a `<style>` tag in the `<head>`. Good for single-page overrides.

```html
<style>
  .special {
    color: green;
  }
</style>
```

### Inline Style

CSS written directly on an element using the `style` attribute. **Strongest specificity**, but hardest to maintain. Avoid unless necessary.

```html
<p style="color: purple;">This is a paragraph</p>
```

#### Key Takeaway: Priority Order

```
Inline > Internal > External
```

> Inline styles override both internal and external styles because they have the highest specificity.

---

## The Cascade & Specificity

CSS applies rules based on **specificity** — a scoring system that decides which rule wins when multiple rules target the same element.

|Selector Type|Specificity Score|
|---|---|
|Inline style|1000|
|ID (`#id`)|100|
|Class (`.class`), Pseudo-class|10|
|Element (`p`, `h1`)|1|

```css
/* Specificity = 1 */
p { color: black; }

/* Specificity = 10 — wins over element selector */
.highlight { color: yellow; }

/* Specificity = 100 — wins over class */
#title { color: red; }
```

> **Common Mistake:** Adding `!important` to "fix" specificity issues. This makes CSS hard to debug. Instead, understand the cascade and write more specific selectors.

---

## Colors

CSS supports multiple color formats — all are equally valid, choose based on context.

```css
/* Color name */
color: red;

/* Hex code — #RRGGBB */
color: #FF5733;

/* Short hex (when pairs repeat) */
color: #F53;    /* same as #FF5533 */

/* RGB */
color: rgb(255, 87, 51);

/* RGB with Alpha (transparency, 0 = invisible, 1 = opaque) */
color: rgb(255 87 51 / 50%);

/* HSL — Hue, Saturation, Lightness */
color: hsl(14, 100%, 60%);
```

> **Tip:** Use **CSS variables** for your color palette so you can change theme colors in one place:

```css
:root {
  --primary: #FF5733;
  --text: #222;
}
p { color: var(--text); }
```

---

## Background

### background-color

```css
background-color: red;
background-color: #FF0000;
background-color: rgb(255 0 0 / 50%);
```

### background-image

```css
background-image: url("../imgs/hero.png");
```

### background-repeat

```css
background-repeat: no-repeat;   /* Show once, no tiling */
background-repeat: repeat-x;    /* Tile horizontally only */
background-repeat: repeat-y;    /* Tile vertically only */
background-repeat: repeat;      /* Tile in both directions (default) */
```

### background-attachment

```css
/* Image scrolls with the page (default) */
background-attachment: scroll;

/* Image is fixed — creates a parallax effect */
background-attachment: fixed;
```

### background-position

```css
background-position: center center;  /* Centered */
background-position: left top;        /* Top-left corner */
background-position: 50% 20%;         /* Custom offset */
```

### background-size

```css
background-size: auto;      /* Original image size */
background-size: cover;     /* Fill container, may crop */
background-size: contain;   /* Fit entirely inside, may leave gaps */
background-size: 300px 200px; /* Explicit dimensions */
```

### Shorthand

```css
/* background: color image repeat attachment position / size */
background: #222 url("hero.png") no-repeat center center / cover;
```

---

## Box Model

Every HTML element is a rectangular box made up of four layers:

```
┌──────────────────────────┐
│         MARGIN           │  ← Space outside the element
│  ┌────────────────────┐  │
│  │      BORDER        │  │  ← The visible border
│  │  ┌──────────────┐  │  │
│  │  │   PADDING    │  │  │  ← Space inside, between content & border
│  │  │  ┌────────┐  │  │  │
│  │  │  │CONTENT │  │  │  │  ← Actual text/image
│  │  │  └────────┘  │  │  │
│  │  └──────────────┘  │  │
│  └────────────────────┘  │
└──────────────────────────┘
```

### Padding

Space **inside** the element, between the content and the border.

```css
/* All four sides */
padding: 10px;

/* Top & Bottom | Left & Right */
padding: 10px 20px;

/* Top | Left & Right | Bottom */
padding: 10px 20px 15px;

/* Top | Right | Bottom | Left (clockwise) */
padding: 10px 20px 15px 25px;

/* Individual sides */
padding-top: 10px;
padding-right: 20px;
padding-bottom: 15px;
padding-left: 25px;
```

### Margin

Space **outside** the element, creating separation between elements.

```css
margin: 20px;
margin: 10px 20px;
margin: auto;       /* Centers block elements horizontally */

/* Negative margins are valid — pull elements closer */
margin-top: -10px;
```

> **Tip:** `margin: 0 auto` is the classic way to center a block element horizontally (requires a defined `width`).

### Border

```css
/* Longhand */
border-width: 2px;
border-style: solid;   /* solid | dashed | dotted | double | none */
border-color: #333;

/* Shorthand */
border: 2px solid #333;

/* Individual sides */
border-top: 3px dashed red;
border-bottom: 1px solid #ccc;
```

### Outline

Similar to border but **does not affect layout** (no space is reserved for it).

```css
outline: 2px solid blue;
outline-offset: 4px;   /* Space between element and outline */
```

> **Common Use:** Outlines are often used for **focus indicators** on interactive elements (important for accessibility). Don't remove `outline: none` without providing an alternative.

---

## Display

The `display` property controls how an element participates in the layout.

```css
display: block;
display: inline;
display: inline-block;
display: none;
display: flex;
display: grid;
```

### Block

```css
div { display: block; }
```

- Takes **full available width** by default.
- Starts on a **new line** (adds line break before and after).
- Respects `width`, `height`, `margin`, and `padding` on all sides.
- Common block elements: `div`, `p`, `h1–h6`, `section`, `article`

### Inline

```css
span { display: inline; }
```

- Takes only as much **width as its content** needs.
- Does **not** start on a new line.
- **Ignores** `width` and `height`.
- **Only respects** horizontal `padding` and `margin` (left & right).
- Common inline elements: `span`, `a`, `strong`, `em`

### Inline-Block

```css
span { display: inline-block; }
```

- Sits **inline** (no forced line break).
- **Respects** `width`, `height`, `padding`, and `margin` on all sides.
- Best of both worlds — use when you need inline elements with box dimensions.

#### Comparison Table

|Property|`block`|`inline`|`inline-block`|
|---|---|---|---|
|New line|✅|❌|❌|
|Full width|✅|❌|❌|
|Respects width/height|✅|❌|✅|
|Respects all margins|✅|❌ (only L/R)|✅|

---

## Visibility

Two ways to hide an element — they behave differently:

```css
/* Removes the element entirely from layout — no space reserved */
display: none;

/* Element is invisible but still occupies space in layout */
visibility: hidden;
```

> **Use Case:** Use `visibility: hidden` when you don't want the page layout to shift when toggling visibility (e.g., keeping a placeholder).

---

## Dimensions

```css
width: 300px;
height: 200px;

/* Responsive constraints */
min-width: 200px;   /* Never shrink below this */
max-width: 800px;   /* Never grow beyond this */
min-height: 100px;
max-height: 500px;

/* Fit the element to its content width */
width: fit-content;

/* Fill available space */
width: 100%;
```

> **Best Practice:** Use `max-width` instead of a fixed `width` for responsive layouts. Combine with `width: 100%` and `margin: auto`:

```css
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}
```

---

## Overflow

Controls what happens when content is **larger than its container**.

```css
overflow: visible;   /* Default — content spills outside (no clipping) */
overflow: hidden;    /* Clips excess content — invisible */
overflow: scroll;    /* Always shows scrollbars */
overflow: auto;      /* Shows scrollbars only when needed (recommended) */

/* Control each axis separately */
overflow-x: hidden;
overflow-y: scroll;
```

> **Common Use:** `overflow: hidden` on a parent is the "clearfix hack" for float-based layouts — it forces the parent to contain floated children.

---

## Text & Typography

### Color & Text Shadow

```css
color: #333;

/* text-shadow: x-offset y-offset blur color */
text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);

/* Multiple shadows */
text-shadow: 1px 1px 0 #000, 2px 2px 0 #555;
```

### Text Alignment

```css
text-align: left;      /* Default for LTR languages */
text-align: right;
text-align: center;
text-align: justify;   /* Stretches text to fill the line width */

/* Page direction — affects layout flow */
direction: ltr;   /* Left to Right (default) */
direction: rtl;   /* Right to Left (Arabic, Hebrew, etc.) */
```

### Vertical Alignment

Aligns **inline** or **inline-block** elements relative to surrounding text:

```css
img {
  vertical-align: middle;  /* top | middle | bottom | baseline */
}
```

### Text Decoration

```css
text-decoration: none;           /* Removes underline (e.g., from links) */
text-decoration: underline;
text-decoration: line-through;   /* Strikethrough */
text-decoration: overline;

/* Shorthand with style and color */
text-decoration: underline dashed red;
```

### Text Transform

```css
text-transform: uppercase;    /* ALL CAPS */
text-transform: lowercase;    /* all lowercase */
text-transform: capitalize;   /* First Letter Of Each Word */
text-transform: none;
```

### Spacing

```css
letter-spacing: 2px;    /* Space between individual characters */
word-spacing: 5px;      /* Space between words */
line-height: 1.6;       /* Space between lines — unitless is recommended */
text-indent: 2em;       /* Indents the first line */
white-space: nowrap;    /* Prevents text from wrapping */
word-break: break-all;  /* Breaks long words to fit container */
```

> **Best Practice:** Use a unitless `line-height` (e.g., `1.5`) so it scales proportionally with the font size.

### Text Overflow

Used when text overflows a container in a single line — creates the "..." effect.

```css
/* Requires these three properties together */
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

### Font Family

```css
/* Serif fonts — have decorative strokes at ends of letters */
font-family: 'Times New Roman', Times, serif;

/* Sans-serif fonts — clean, no strokes */
font-family: Arial, Helvetica, sans-serif;

/* Google Fonts (import in <head> first) */
font-family: 'Roboto', sans-serif;
```

> **Tip:** Always end your font stack with a generic family (`serif`, `sans-serif`, `monospace`) as a fallback.

### Font Size & CSS Units

```css
font-size: 16px;    /* Pixels — absolute, predictable */
font-size: 1em;     /* Relative to parent's font size (1em = parent size) */
font-size: 1rem;    /* Relative to root (<html>) font size — more predictable */
font-size: 100%;    /* Percentage of parent's font size */
font-size: 5vw;     /* 5% of the viewport width — responsive */
```

#### CSS Units Summary

|Unit|Relative To|Use Case|
|---|---|---|
|`px`|Screen pixels|Fixed sizes, borders|
|`em`|Parent's font size|Component-level scaling|
|`rem`|Root (`<html>`) font size|Global consistent sizing|
|`%`|Parent element|Fluid layouts|
|`vw`|Viewport width|Full-width responsive elements|
|`vh`|Viewport height|Full-screen sections|

### Font Style, Weight & Variant

```css
font-style: normal;
font-style: italic;

font-weight: normal;   /* 400 */
font-weight: bold;     /* 700 */
font-weight: 300;      /* Light */
font-weight: 900;      /* Extra Bold */

font-variant: small-caps;   /* Displays lowercase as small uppercase letters */
```

---

## Inheritance

Some CSS properties **inherit** their value from the parent element automatically (e.g., `color`, `font-family`, `font-size`). Others do not (e.g., `border`, `margin`, `padding`).

```css
/* Force any property to inherit from parent */
color: inherit;
border: inherit;
```

```html
<!-- Example: child inherits color from parent -->
<div style="color: red;">
  <p>This text will be red (inherited).</p>
</div>
```

---

## Mouse Cursor

```css
cursor: pointer;    /* Hand — use for clickable elements */
cursor: default;    /* Default arrow */
cursor: text;       /* Text input beam */
cursor: not-allowed; /* Indicates disabled state */
cursor: grab;       /* For draggable elements */
```

---

## Float & Clear

`float` was historically used for layouts but is now mainly used for **text wrapping around images**. For layouts, use **Flexbox** or **Grid**.

```css
img {
  float: left;    /* Text wraps to the right of the image */
  margin-right: 15px;
}
```

### Clearing Floats

Floated elements are removed from normal flow, which can collapse their parent container. Use `clear` to fix this:

```css
.clearfix {
  clear: both;    /* Stops wrapping — both | left | right */
}
```

```html
<div class="parent">
  <div style="float: left;">Item 1</div>
  <div style="float: left;">Item 2</div>
  <div class="clearfix"></div>  <!-- Resets flow -->
</div>
```

> **Modern Alternative:** Instead of the clearfix hack, set `overflow: hidden` or `display: flow-root` on the parent:

```css
.parent {
  overflow: hidden; /* Contains floated children */
}
```

---

## CSS calc()

Allows you to perform **math operations** in CSS, mixing different units.

```css
width: calc(100% - 60px);
padding: calc(1rem + 5px);
```

**Real-world use case — Equal-width columns with gaps:**

```css
/* 5 columns with 10px gaps between them (6 gaps total = 60px) */
.column {
  float: left;
  width: calc((100% - 60px) / 5);
  margin-left: 10px;
}
```

> **Operators:** `+`, `-`, `*`, `/` — always add spaces around `+` and `-` operators!

---

## Opacity

Controls transparency of an **entire element** (including children).

```css
/* 0 = fully transparent, 1 = fully opaque */
opacity: 0.5;   /* 50% transparent — affects the whole element */
```

**vs. RGB alpha channel** — only affects the background color, not child content:

```css
/* Only the background is 50% transparent — text remains fully visible */
background-color: rgb(255 0 0 / 0.5);
```

> **Key Difference:** `opacity` makes everything (text, children, borders) transparent. `rgba`/`rgb(.../ alpha)` only affects that specific color.

---

## Position

Controls how an element is placed in the page layout.

```css
position: static;    /* Default — normal document flow */
position: relative;  /* Offset from its normal position */
position: absolute;  /* Positioned relative to nearest non-static ancestor */
position: fixed;     /* Fixed to viewport — stays visible while scrolling */
position: sticky;    /* Sticks at a threshold when scrolling */
```

### static (Default)

Element flows normally. `top`, `left`, `right`, `bottom` have no effect.

### relative

Element stays in the flow but can be nudged with offset properties.

```css
.box {
  position: relative;
  top: 10px;   /* Move 10px down from original position */
  left: 20px;  /* Move 20px right from original position */
}
```

> Also used to make a container the **reference point** for absolutely positioned children.

### absolute

Removed from normal flow. Positioned relative to the **nearest ancestor with a non-static position**.

```css
.parent {
  position: relative;  /* Acts as the reference frame */
}
.child {
  position: absolute;
  top: 0;
  right: 0;   /* Placed at top-right corner of .parent */
}
```

### fixed

Removed from flow. Positioned relative to the **viewport** — doesn't move on scroll.

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
```

### sticky

Behaves like `relative` until you scroll to a threshold, then behaves like `fixed`.

```css
.section-header {
  position: sticky;
  top: 0;   /* Sticks when it reaches the top of the viewport */
}
```

---

## Z-index

Controls the **stacking order** of positioned elements (which appears on top).

- Higher value = on top.
- Only works on elements with a non-static `position`.

```css
.one {
  position: absolute;
  background-color: red;
  z-index: 3;   /* On top */
}
.two {
  position: absolute;
  background-color: green;
  z-index: 2;
}
.three {
  position: absolute;
  background-color: blue;
  z-index: 1;   /* Behind */
}
```

> **Tip:** Avoid arbitrary large z-index values like `z-index: 9999`. Use a scale (1, 2, 3...) or CSS variables to manage layers.

---

## Lists & Tables

### List Styling

```css
/* Remove default bullets */
ul {
  list-style: none;
  padding: 0;
}

/* Shorthand: type | position | image */
list-style: square inside url("bullet.png");

list-style-type: disc;     /* • */
list-style-type: circle;   /* ○ */
list-style-type: square;   /* ■ */
list-style-type: decimal;  /* 1, 2, 3 */
```

### Table Styling

```css
table {
  width: 100%;
  border-collapse: collapse;   /* Merges double borders into one */
  border-spacing: 0;
}
td, th {
  padding: 12px 15px;
  border: 1px solid #ccc;
  text-align: left;
}
thead tr {
  background-color: #f44336;
  color: white;
  font-weight: bold;
  text-align: center;
}
tbody tr:nth-child(even) {
  background-color: #f5f5f5;  /* Zebra striping for readability */
}
tbody tr:hover {
  background-color: #e0e0e0;  /* Row hover highlight */
}
```

---

## Pseudo-Classes

Target elements based on their **state** or **position** — no class needed in HTML.

```css
/* Link states */
a:link    { color: blue; }       /* Unvisited link */
a:visited { color: purple; }     /* Visited link */
a:hover   { color: red; }        /* Mouse is over the element */
a:active  { color: orange; }     /* Being clicked */

/* Form states */
input:focus  { border-color: blue; outline: none; }
input:checked { display: none; }
input:disabled { opacity: 0.5; }

/* Structural pseudo-classes */
li:first-child  { font-weight: bold; }
li:last-child   { border-bottom: none; }
li:nth-child(2) { color: red; }
li:nth-child(odd)  { background: #f0f0f0; }
li:nth-child(even) { background: #fff; }

/* Empty elements */
:empty { border: 2px dashed red; }
```

---

## Pseudo-Elements

Target a **specific part** of an element or insert virtual content.

```css
/* Style the first letter */
p::first-letter {
  font-size: 3em;
  font-weight: bold;
  float: left;
  margin-right: 4px;
}

/* Style the first line */
p::first-line {
  font-weight: bold;
  color: navy;
}

/* Style selected text */
::selection {
  background-color: black;
  color: yellow;
}
```

### `::before` and `::after`

Insert virtual elements **before** or **after** an element's content. Requires `content` property.

```css
/* Add decorative quotes */
blockquote::before { content: "\201C"; }   /* " */
blockquote::after  { content: "\201D"; }   /* " */

/* Common pattern: decorative triangle using borders */
.tooltip::before {
  content: "";
  position: absolute;
  top: 50%;
  left: -10px;
  margin-top: -5px;
  border: 5px solid transparent;
  border-right-color: #333;
}
```

### `content` Values

```css
/* String */
content: "Read more →";

/* Attribute value */
content: attr(data-label);   /* Reads from data-label="..." on the element */

/* Counter */
.parent { counter-increment: section; }
.parent::after { content: counter(section); }

/* Empty (for decorative boxes) */
content: "";
```

---

## Vendor Prefixes

Some newer CSS features required **browser-specific prefixes** during experimental phases before becoming standard.

|Prefix|Targets|
|---|---|
|`-webkit-`|Chrome, Safari, modern Opera|
|`-moz-`|Firefox|
|`-ms-`|Internet Explorer, Edge (old)|
|`-o-`|Old Opera|

```css
.box {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  border-radius: 10px;   /* Standard — always put LAST */
}
```

> **Modern Reality:** Most modern CSS features no longer need prefixes. Tools like **Autoprefixer** or VS Code extensions can add them automatically. Always include the unprefixed version last.

---

## Border Radius

Rounds the corners of an element's border.

```css
border-radius: 6px;         /* All corners */
border-radius: 10px 0;      /* Top-left & bottom-right | top-right & bottom-left */
border-radius: 50%;          /* Creates a circle (on a square element) */

/* Individual corners */
border-top-left-radius: 10px;
border-top-right-radius: 5px;
border-bottom-right-radius: 10px;
border-bottom-left-radius: 5px;

/* Elliptical corners (horizontal-radius / vertical-radius) */
border-radius: 50px / 20px;
```

---

## Box Shadow

Adds shadow effects to elements. Multiple shadows can be layered.

```css
/* Syntax: h-offset v-offset blur spread color inset */
box-shadow: 2px 4px 8px 0 rgba(0, 0, 0, 0.2);

/* Inner shadow */
box-shadow: inset 0 2px 4px rgba(0,0,0,0.3);

/* Multiple shadows (layered) */
box-shadow:
  0 1px 3px rgba(0,0,0,0.12),
  0 1px 2px rgba(0,0,0,0.24);
```

|Value|Description|
|---|---|
|`h-offset`|Horizontal shadow position (positive = right)|
|`v-offset`|Vertical shadow position (positive = down)|
|`blur`|Blur radius — larger = softer shadow|
|`spread`|Expands or shrinks the shadow|
|`color`|Shadow color|
|`inset`|Makes shadow appear inside the element|

---

## Box Sizing

Controls **how `width` and `height` are calculated**.

```css
/* Default — width/height = CONTENT ONLY. Padding & border add to total size. */
box-sizing: content-box;

/* width/height = includes padding and border. Much more intuitive. */
box-sizing: border-box;
```

**Example:**

```css
/* content-box (default): total width = 200px + 20px + 4px = 224px */
.box {
  box-sizing: content-box;
  width: 200px;
  padding: 10px;
  border: 2px solid black;
}

/* border-box: total width = exactly 200px */
.box {
  box-sizing: border-box;
  width: 200px;
  padding: 10px;
  border: 2px solid black;
}
```

> **Best Practice:** Apply `border-box` globally at the top of your stylesheet:

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

---

## Grouping & Nesting Selectors

### Grouping

Apply the same styles to multiple selectors by separating them with commas:

```css
h1, h2, h3, h4 {
  font-family: Georgia, serif;
  color: #222;
}

.card, .panel, .modal {
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

### Nesting (Descendant Selector)

Target elements **inside** other elements without needing extra classes:

```css
/* Only targets <p> elements that are INSIDE a <div> */
div p {
  color: gray;
}

/* Only targets .special inside a div (not .special elsewhere) */
div .special {
  color: red;
}

/* Direct child only (not grandchildren) */
div > p {
  font-weight: bold;
}

/* Adjacent sibling — p immediately after h2 */
h2 + p {
  font-size: 1.2em;
}
```

---

## Resources

- [CSS Course — Elzero Web School](https://elzero.org/category/courses/css-course/)
- [CSS Useful Features — Elzero Web School](https://elzero.org/category/courses/css-features/)
- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [CSS Tricks](https://css-tricks.com/)