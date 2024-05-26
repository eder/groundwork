# Principles for Writing Consistent and Idiomatic CSS with Groundwork

The following document outlines a sensible style guide for CSS development. I do not intend to be prescriptive and do not wish to impose my stylistic preferences on others' code. However, these guidelines strongly encourage the use of existing, common, and sensible standards.

This is a living document, and new ideas are always welcome.

## Table of Contents

1. [General Principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [Formatting](#format)
5. [Naming](#naming)
6. [Practical Example](#example)
7. [Organization](#organization)

<a name="general-principles"></a>
## 1. General Principles

> "Part of being a good steward of a successful project is realizing that writing code just for yourself is a Bad Idea™. If thousands of people are using your code, then write it with maximum clarity, not according to your personal preferences for being clever with the specification." - Idan Gazit

* All code in any application should look as if it was written by a single person, regardless of how many people contributed.
* Enforce the agreed-upon style rigorously.
* When in doubt, use existing and common standards.

<a name="whitespace"></a>
## 2. Whitespace

Only one style should exist throughout the project. Always be consistent with the use of whitespace. Use whitespace to improve readability.

* _Never_ mix spaces and tabs for indentation.
* Choose between soft indentation (spaces) or hard indentation (tabs). Stick to your choice without fail. (Preference: spaces)
* If using spaces, choose the number of characters per indentation level. (Preference: 4 spaces)

Tip: Configure your editor to "show invisibles." This will allow you to eliminate trailing whitespace, eliminate whitespace from empty lines without indentation, and avoid polluted commits.

Tip: Use an [EditorConfig](http://editorconfig.org/) file (or equivalent) to help maintain the basic whitespace conventions you have agreed upon for your codebase.

<a name="comments"></a>
## 3. Comments

Well-commented code is extremely important. Take the time to describe components, how they work, their limitations, and how they are constructed. Do not leave others on the team guessing the purpose of uncommon or non-obvious code.

Comment style should be simple and consistent within a single codebase.

* Place comments on a new line above their subject.
* Avoid end-of-line comments.
* Keep line length to a sensible maximum, e.g., 80 columns.
* Use liberal comments to break the CSS code into distinct sections.
* Use capitalized comments and consistent text indentation.

Tip: Configure your editor to provide shortcuts for generating the agreed-upon comment style.

#### Example with CSS:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/*
 * Group comment block
 * Ideal for multi-line explanations and documentation.
 */
 
/**
 * Brief description using Doxygen comment style
 *
 * The first sentence of the long description starts here and continues
 * on this line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and documentation.
 * It can include HTML examples, URLs, or any other information
 * considered necessary or helpful.
 *
 * @tag This is a tag called 'tag'
 *
 * @todo This is a task statement that describes an atomic task to be 
 * completed at a later date. It wraps after 80 characters, and the following lines 
 * are indented by two spaces.
 */

/* Basic comment */
```

#### Example with SCSS:

```scss
// ==========================================================================
// Section comment block
// ==========================================================================

// Sub-section comment block
// ==========================================================================

//
// Group comment block
// Ideal for multi-line explanations and documentation.
//

// Basic comment
```

<a name="format"></a>
## 4. Formatting

The chosen code format should ensure that the code is: easy to read; easy to comment on clearly; minimizes the chance of accidentally introducing errors; and results in useful diffs.

* One discrete selector per line in multi-selector rule sets.
* A single space before the opening brace in a rule set.
* One declaration per line in a declaration block.
* One level of indentation for each declaration.
* A single space after the colon in a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes, e.g., `content: " "`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function values.
* Always include a trailing semicolon in the last declaration of a declaration block.
* Place the closing brace of a rule set in the same column as the first character of the rule set.
* Separate each rule set by a blank line.

```css
.selector-1,
.selector-2,
.selector-3 {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    color: #333;
    background: #fff;
}
```

#### Declaration Order

Declarations should be ordered according to a single principle. My preference is for related properties to be grouped and for structurally important properties (e.g., positioning and box-model) to be declared before typographic, background, or color properties.

```css
.selector {
    /* Positioning */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* Display & Box Model */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    /* Other */
    background: #000;
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;
}
```

Alphabetical ordering is also popular, but the downside is that it separates related properties. For example, positioning offsets are no longer grouped, and box-model properties can end up spread throughout a declaration block.

#### Exceptions and Minor Deviations

Large blocks of single declarations may use a different style, formatting on a single line. In this case, a space should be considered after the opening brace and before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or shadows - can be arranged across multiple lines to improve readability and produce more useful diffs. Various formats could be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```

#### Miscellaneous

* Use lowercase hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes, e.g., `content: ""`.
* Always quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero values, e.g., `margin: 0`.

### Preprocessors: Additional Formatting Considerations

Different CSS preprocessors have different features, functionalities, and syntax. Your conventions should be extended to accommodate the particularities of any preprocessor in use. The following guidelines reference Sass.

* Limit nesting to 1 level deep. Reevaluate any nesting that is more than 2 levels deep. This prevents overly specific CSS selectors.
* Avoid a large number of nested rules. Break them up when readability starts to be affected. Preference is to avoid nesting that spreads over more than 20 lines.
* Always place `@extend` statements at the top of a declaration block.
* When possible, group `@include` statements at the top of declaration blocks, after any `@extend` statements.
* Consider custom functions for prefixes with `x-` or any namespace. This helps avoid potential confusion with native CSS functions or conflicts with library functions.

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
    // other declarations
}
```

<a name="naming"></a>
## 5. Naming

You are not a human code compiler/minifier, so don't try to be.

Use clear and purposeful names for HTML classes. Choose a naming pattern that is understandable and consistent, making sense for both HTML and CSS files.

In this project, we will use domain and intent conventions, including some standardizations from BEM and SMACSS.

```css
/* Example of bad names */

.s-scr {
    overflow: auto;
}

.cb {
    background: #000;
}

/* Example of good names */

.is-scrollable {
    overflow: auto;
}

.column-body {
    background: #000;
}

/* Example of domain and intent */
.home-container {
    width: 960px;
}

/* Use underscore for derived words or sub-modules */
.home-header_navigation {
    background: gray;
} 

/* Use double underscores for nested or direct

 descendants */
.home-header_navigation__item {
    display: inline-block;
}

/* Use -- for modifier elements */
.home-header_navigation--secondary {
    background: red;
    height: 30px;
    width: 100%;
}
```

<a name="example"></a>
## 6. Practical Example

An example showcasing various conventions.

```css
/* ==========================================================================
   Grid layout
   ========================================================================== */

/*
 * Horizontal scroll column layout.
 *
 * This creates a single full-height, non-wrapping row of columns that can
 * be horizontally scrolled within their parent.
 *
 * HTML Example:
 *
 * <div class="grid">
 *     <div class="cell cell-5"></div>
 *     <div class="cell cell-5"></div>
 * </div>
 */
 
/**
 * Grid container
 * Must contain only `.cell` children
 */

.grid {
    overflow: visible;
    height: 100%;
    /* Prevent inline-block cells from wrapping */
    white-space: nowrap;
    /* Remove inter-cell whitespace */
    font-size: 0;
}

/**
 * Grid cells
 * Default width is not explicit. Extend with `.cell-n` classes.
 */

.cell {
    box-sizing: border-box;
    position: relative;
    overflow: hidden;
    width: 20%;
    height: 100%;
    /* Set the inter-cell spacing */
    padding: 0 10px;
    border: 2px solid #333;
    vertical-align: top;
    /* Reset white-space */
    white-space: normal;
    /* Reset font-size */
    font-size: 16px;
}

/* Cell states */

.cell.is-animating {
    background-color: #fffdec;
}

/* Cell dimensions
   ========================================================================== */

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }

/* Cell modifiers
   ========================================================================== */

.cell--detail,
.cell--important {
    border-width: 4px;
}
```

<a name="organization"></a>
## 7. Organization

Code organization is an important part of any CSS codebase, and crucial for large codebases.

* Logically separate distinct parts of the code.
* Use separate files (concatenated by a build process) to help break up code for distinct components.
* If using a preprocessor, abstract common parts of the code into variables for color, typography, etc.
