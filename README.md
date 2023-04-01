# HTML & CSS

DOCTYPE Declaration

```html
<!DOCTYPE html>
```

This tells the browser that this document is html5 document.

---

`<head>` tag is used to give browser information about the page (nothing will be rendered).

---

`/` always shows the root of our site  
we can use `/` for absolute path

---

## HTML Entities

We use "HTML Entities" to show special characters.  
All HTML entities start with `&` and end with `;`

---

## WebPage Structure

Sometimes we can have a **sidebar** for advertising or content that is not directly related to the **main content**.

```html
<body>
    <header>
        <nav>
            <ul>
                <li></li>
                <li></li>
                <li></li>
            </ul>
        </nav>
    </header>
    <main>
        <section>
            <h2>Products</h2>
            <article></article>
            <article></article>
            <article></article>
        </section>
        <section>
            <h2>Testimonial</h2>
            <article>
                <section></section>
                <section></section>
                <section></section>
            </article>
            <article></article>
        </section>
    </main>
    <!-- 
        Sometimes we can have a sidebar
        for advertising or content
        that is not directly related
        to the main content
    -->
    <aside></aside>
    <footer>
        <nav>
            <ul>
                <li></li>
                <li></li>
                <li></li>
            </ul>
        </nav>
    </footer>
</body>
```

---

## Pseudo class and Pseudo element

Browser by default add some classes to elements e.g. The first child element has "first-child" class These are called "**_Pseudo-class_**".

**THESE ARE NOT REAL CLASSES** because of that
they called "PSEUDO_CLASS"

Pseudo-class select specific state of an element  
Pseudo-elements are used to select a part of an element

**style.css**

```css
body {
    margin: 10px;
}

article :first-of-type {
    font-size: 140%;
    font-style: italic;
}

article p:last-child {
    font-weight: bold;
}

a:visited,
a:link {
    color: dodgerblue;
}

a:hover,
a:focus {
    color: deeppink;
}

ul li:nth-child(even) {
    color: deeppink;
}

.element::first-letter {
    font-size: 140%;
    font-weight: bold;
}

::selection {
    background-color: pink;
}

p::before {
    content: "...";
    display: block;
}
```

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <link rel="stylesheet" href="css/normalize.css" />
        <link rel="stylesheet" href="css/styles.css" />
    </head>

    <body>
        <article>
            <h1>Heading</h1>
            <p>Lorem ipsum dolor sit amet.</p>
            <p>Lorem ipsum dolor sit amet.</p>
            <a href="https://someweirdwebsite.com">Link</a>
            <ul>
                <li>Item 1</li>
                <li>Item 2</li>
                <li>Item 3</li>
                <li>Item 4</li>
                <li>Item 5</li>
            </ul>
            <p class="element">
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed
                atque molestiae est dicta a at nemo porro, pariatur aut,
                consectetur, aliquid doloremque? Doloribus odio soluta, saepe
                architecto, provident sint voluptatibus laborum numquam omnis
                est velit atque voluptatem facilis praesentium distinctio
                voluptate adipisci. Optio amet possimus sapiente voluptatibus
                quo ullam nesciunt?
            </p>
        </article>
    </body>
</html>
```

---

## Selector Specificity (Weight)

Each selector has what we call a specificity or weight.  
If multiple rules target the same element browser will apply the rule that is more specific.  
**Selector Specificty**

1. ID Selector (#products)
2. Class & Attribute Selectors
3. Element Selector

_vscode_ has something that shows selector specificity (ID, Class / Attribute, Element)

```css
/* (0, 0, 1) */
h1 {
    color: green;
}
/* (0, 1, 0) */
.highlight {
    color: blue;
}
/* (1, 0, 0) */
#products {
    color: red;
}
/* (1, 1, 1) */
h1.highlight #products {
    color: brown;
}
```

---

## Inheritance

In CSS properties are inherited from parent elements by default.  
So there is no need to mention those properties again for child elements.  
**How to stop inheritance ?**  
Just by setting the child property to `initial`.

```css
p {
    color: dodgerblue;
}
/* 
In this case, the "strong" tag doesn't inherit the color value from the "p" tag
 */
strong {
    color: initial;
}
```

```html
<body>
    <p>Lorem ipsum <strong>dolor</strong> sit amet.</p>
</body>
```

Some properties don't get inherited from the parent element because it doesn't make sense.  
For example, the border property doesn't inherit from the parent element, but we can force it to inherit by setting the child property to `inherit`.

```css
p {
    color: dodgerblue;
    border: 1px solid black;
}

strong {
    color: initial;
    border: inherit;
}
```

---

## Gradients

Gradients are technically _images_.  
So we cannot use the `background-color` property for setting gradients instead we should either use the `background-image` or `background` properties.

---

## Margin Collapsing

If we have two elements up and down each other their margins get collapsed into a single margin.  
Top and bottom margins of elements are sometimes collapsed into a single margin that is equal to the largest of the two margins.  
_This does not happen on **left** and **right** margins! Only **top** and **bottom** margins!_  
The horizontal margins never collapse.  
So technically we should use the margin property to separate elements.

```html
<style>
    p {
        margin-top: 10px;
        margin-bottom: 10px;
    }
</style>

<main>
    <!-- 10px margin -->
    <p>My First Paragraph</p>
    <!-- 10px margin (collapsed) -->
    <p>My Second Paragraph</p>
    <!-- 10px margin (collapsed) -->
    <p>My Third Paragraph</p>
    <!-- 10px margin -->
</main>
```

To avoid conflict with _margin collapse_, One possible solution that it is easy to remember and understand is only applying margin-top to the elements.

```html
<style>
    p {
        margin-top: 10px;
    }
</style>

<main>
    <!-- 10px margin -->
    <p>My First Paragraph</p>
    <!-- 10px margin -->
    <p>My Second Paragraph</p>
    <!-- 10px margin -->
    <p>My Third Paragraph</p>
    <!-- 0 margin -->
</main>
```

---

**_Universal Selector_** doesn't select pseudo-elements so rules don't apply to pseudo-elements.  
So we have to choose them ourselves.

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

Browsers by default set button elements `box-sizing` to `border-box`.

Spaces, before span tags, will normalize into a single space and we will have a bit of space between elements in the rendered document.

```html
<body>
    <span class="box"></span>
    <span class="box"></span>
</body>
```

In order to avoid this unwanted distance, we have to remove spaces between span tags and put them together.

```html
<body>
    <span class="box"></span><span class="box"></span>
</body>
```

---

## Measurement Units

There are two types of measurement units:

-   Absolute
    -   px
-   Relative
    -   %  
         _relative to the size of the container_
    -   vw
    -   vh  
         _relative to the viewport_
    -   em
    -   rem  
         _relative to the font size_

```css
html {
    /* 62.5% of 16px = 10px */
    font-size: 62.5%;
}

.box {
    /* 
    based on the font-size of the root element
    .box width will be 150px (15 * 10)
  */
    width: 15rem;
}
```

---

## Positioning

-   Relative:  
     relative to the element's normal position
-   Absoulte:  
    relative to the parent
-   Fixed:
    relative to the viewport

---

## Floating Elements

CSS float property causes the element to float to one side of its container element and subsequent elements will flow around it.

Parent elements doesn't see floated elements.  
This called **parent collapsing** and you should clear float.  
You shouldn't use float to build layout instead use Grid and Flexbox.

```css
.avatar {
    width: 5rem;
    height: 5rem;
    background-color: gold;
    /* 
    This property make the avatar element to float to the left side of its container element.
     */
    float: left;
}
```

---

## Flexbox

Flexible Box Layout (FlexBox)  
Used for laying out elements in _one direction_.

Directions:

-   Row
-   Column

Axes in Flex:

-   Main (Primary)
-   Cross (Secondary)

These Axes are dependent on the direction.

-   Direction Row:  
    Main: _Row_ , Cross: _Column_
-   Direction Column:  
    Main: _Column_ , Cross: _Row_

Aligning Items:

-   justify-content (along the **main** axis)
-   align-items (along the **cross** axis)
-   _align-content_

### what is align-content?

This property only works if we have multiple lines in our flex container.

The default behavior of the flex container doesn't wrap items in a new line so flex items get smaller and deformed.

So we need to use the `flex-wrap` property to wrap extra items on a new line and in this way flex items keep their original size.

**But** if we use the center for the vertical axis in the flex container (`align-items`) there is a problem.

when we had a single line we put our element in the center of the vertical axis but now that we have multiple lines our elements are not quite in the center and the first line is closer to the beginning of the vertical axis and the second line is closer to the end.

**_NOW_** this is where the `align-content` property comes into play, with this property we can align multiple lines or the entire content as a whole.  
So we can put the entire content in the center of the vertical axis.

```css
.container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    align-content: center;
}
```

Sizing Items:

-   flex-basis (the initial size of a flex item)
-   flex-grow (the growth factor)
-   flex-shrink (the shrink factor)
-   flex (shorthand)

All these properties should be applied to flex items.

---

## Grid

We use _grid_ to lay out elements in both rows and columns.  
A very common application of grid is in creating photo galleries.

Defining a grid:

-   display: grid
-   grid-template-rows
-   grid-template-columns

Grid items by default are aligned to the top left corner of its containing cell but we can easily align these items along the horizontal or vertical axis.

Aligning items:

-   justify-items (along the **horizontal** axis)
-   align-items (along the **vertical** axis)

```css
.container {
    display: grid;
    grid-template: repeat(3, 100px) / repeat(2, 100px);
    justify-items: center;
    align-items: center;
    border: 3px solid lightgrey;
}
```

Note that if we don't set `width` and `height` properties for grid items they will stretch to filling the cell.

```css
.container {
    /* 
    These are default values
  */
    justify-items: stretch;
    align-items: stretch;
}
```

The grid is aligned to the left side of its container but we have two extra properties for aligning the grid inside its container.

Aligning grid:

-   justify-content (along the **horizontal** axis)
-   align-content (along the **vertical** axis)

Grid items gap:

-   row-gap (gap between each row)
-   column-gap (gap between each column)
-   gap (shorthand property [row gap] [column gap])

Placing grid items (these properties are for items only):

-   grid-row
-   grid-column
-   grid-area

Placing items in named areas:

-   grid-template-areas -> grid container
-   grid-area -> grid item

```css
.container {
    display: grid;
    grid-template: repeat(3, 100px) / repeat(2, 100px);
    grid-template-areas:
        "header  header"
        "sidebar main"
        ".       footer";
}

.box-one {
    grid-area: header;
}
```

---

## Media Queries

With the help of media queries we can provide different styles for different devices depending on their features.

Approaches for responsive design:

-   Desktop first
-   Mobile first

A **breakpoint** is the point at which our design breaks.

---

## Styling Fonts

We have three main categories of fonts.  
Font categories:

-   Serif

    they have small line at the end of characters

    -   Georgia
    -   Time New Roman

-   Sans-serif

    they are more playful and modern

    -   Avenir
    -   Arial
    -   Futura
    -   Helvetica
    -   Roboto

-   Monospace

    monospace means _one space_  
    width of all characters is exactly the same and that's why these fonts are ideal for displaying code.

    -   Consolas
    -   Courier
    -   Ubuntu

Font stack consists of multiple fonts.

```css
p {
    font-family: Arial, Helvetica, sans-serif;
}
```

sans-serif is a generic font and the actual font that will be used will vary from one computer to another so we just type a generic name and let the browser decide what font should be used.

### Font formats

-   TTF
-   OTF
-   EOT
-   WOFF
-   WOFF 2.0

---

## Vertical spacing

-   margin
-   line-height  
     The general rule of thumb is to set this to one and half times the font size.  
     If we supply a line hight _without_ a unit this will be used as multiplier

### Law of Proximity:

The law of proximity describes how we humans see connections between various objects so _Objects that are closer are preceived to be related_.

---

## Horizontal spacing

-   letter-spacing (control space between letters in text)
-   word-spacing (control space between words in text)
-   width

**Ideal line length** should be between 50 - 70 character.

For achieving that we can use `ch` CSS unit.  
`ch` is another unit in CSS which is relative to the width of the **ZERO** character (0).  
`50ch` is equivalent to 50 zeros.

But, why 50 zeros?  
Because characters like _i_ or _1_ take less space but if we have 50 zeros it's roughly equivalent to 60 to 70 characters.

```css
p {
    width: 50ch;
}
```

---

## Formatting text

Formatting text properties:

-   text-align (control the horizontal alignment of text)
-   text-indent (adding indentation on the first line of out text)
-   text-decoration
-   text-transform
-   white-space (used for controling wrapping)
-   column-\* (used for creating multi column text)
    -   column-count (create `x` columns of text)
    -   column-gap (gap between columns)
    -   column-rule (rule between columns)
-   direction (used for direction of languages)

For truncating text we need the below properties.

```css
p {
    width: 50ch;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

---

## Image types

-   Raster image - made of pixels
    -   Come from cameras/scanners
    -   Formats: JPG, PNG, GIF, etc
    -   More pixels = larger file size
    -   Lokk blurry if scaled up
-   Vector image - made of vectors
    -   Create in software (Illustrator)
    -   Format: SVG
    -   Scalable Vector Graphics
    -   Look sharp at any size

| Format | Color | Transparency | Animation |
| :----: | :---: | :----------: | :-------: |
|  JPG   |  16M  |              |           |
|  GIF   |  256  |     YES      |    YES    |
|  PNG   |  16M  |     YES      |    YES    |
|  WebP  |  16M  |     YES      |    YES    |

---

## Type of images in HTML

In html we have two types of images:

-   content images
-   background images

---

## CSS Sprites

CSS Sprites is an optimization technique.

---

## Data URLS

Formerly: Data URIs  
Another optimization techique to reduce HTTP requests.  
With this technique we can embed an image directly into an HTML document or style sheet.

data is another protocol which is used for representing a binary file in a sequence of characters.

Problems:

-   Size of embedded code > size of the resource
-   Increased complexity
-   Slow on mobile

## High Density Screens

We should provide images for different DPRs.  
If DPR > 1 so it's High Density Screen

```html
<img
    src="images/meal.jpg"
    alt=""
    class="meal"
    srcset="images/meal.jpg 1x, images/meal@2x.jpg 2x, images/meal@3x.jpg 3x"
/>
```

---

### Forms

### DataLists

We can use datalists to assign a predefined list to input element.

```html
<form>
    <input type="text" list="countries" autocomplete="off" />
    <datalist id="countries">
        <option data-value="1">Australia</option>
        <option data-value="2">Canada</option>
        <option data-value="3">India</option>
        <option data-value="4">United States</option>
    </datalist>
</form>
```

### Option group in forms

```html
<form>
    <select>
        <optgroup label="Front-end Courses">
            <option value="1">HTML</option>
            <option value="2">CSS</option>
            <option value="3">JavaScript</option>
        </optgroup>
        <optgroup label="Back-end Courses">
            <option value="1">Node.js</option>
            <option value="2">ASP.NET</option>
            <option value="3">Django</option>
        </optgroup>
    </select>
</form>
```

### Radio Button

Using `name` in radio buttons group theme.

```html
<form>
    <div>
        <input type="radio" name="member-ship" id="silver" />
        <label for="silver" class="label-inline">Silver</label>
    </div>
    <div>
        <input type="radio" name="member-ship" id="gold" />
        <label for="gold" class="label-inline">Gold</label>
    </div>
</form>
```

### Fieldset

Fieldset is a way for grouping related fields.

```html
<form>
    <fieldset>
        <legend>Billing Address</legend>
        <input type="text" />
        <input type="text" />
        <input type="text" />
    </fieldset>
    <fieldset>
        <legend>Payment</legend>
        <input type="text" />
        <input type="text" />
        <input type="text" />
    </fieldset>
</form>
```

### Action

Action in forms shows where we are sending the data.

---

## Transformation

Before using transform functions on Z axis we should define perspective.  
Perspective define a virtual distance between element and us.

```css
.container:hover .box {
    transform: perspective(200px) rotateY(45deg);
    transform-origin: 0 50%;
}
```

This property will shared between parent and children elements.

```css
.container {
    perspective: 200px;
}

.container:hover .box {
    transform: rotateY(45deg);
    transform-origin: 0 50%;
}
```

---

## Clean CSS

Best Practices:

-   Follow a naming convention
    -   kebab-case
    -   camelCase
    -   PascalCase
    -   snake_case  
        There is no difference between conventions.
-   Create logical sections in your stylesheet

    ```css
    /* Basic styles */

    * {
        box-sizing: border-box;
    }

    html {
    }

    /* Typographys */

    /* Forms */

    /* Naviation Bar */
    ```

    If your project is a big project you create a separate file for each style section

-   Avoid over-specific selectors

    ```css
    div.nav > ul.items > li {
    }
    ```

    This is wrong

-   Avoid `!important`
-   Sort CSS properties  
    select properties and open command palette and search for sort
-   Take advantage of style inheritance

    ```css
    .nav {
        font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    }

    .nav-item {
    }

    .nav-brand {
    }
    ```

-   Extract repetitive patterns
-   Avoid repetitive values (Keep it DRY)

### Object-oriented CSS

```css
.hero .btn {
    background: gold;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}

.side-bar .btn {
    background: gold;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}
```

### Separate container and content

content is `.btn` and container is `.hero`.  
So we change ugly and wrong top styles to this.

```css
.btn {
    background: gold;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}
```

### Separate structure and skin

From this.

```css
.btn {
    background: gold;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}

.btn-blue {
    background: dodgerblue;
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}
```

To this.

```css
.btn {
    border: 0;
    border-radius: 30px;
    padding: 1rem 2rem;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serifs;
}

.btn-primary {
    background-color: gold;
}

.btn-secondary {
    background-color: dodgerblue;
}
```

Here background color is skin.

## BEM

Block Element Modifier

---

## Famous components

-   Hero / Banner section
-   Media component / object
-   Callout component

---

## Steps to create a component

1. Create _color palette_
2. Add _typography_
3. Detect and Add _components_
