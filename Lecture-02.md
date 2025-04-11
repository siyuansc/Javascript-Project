---
marp: true
theme: default
paginate: true
---

# SI 379
## Building Interactive Applications

Lecture 2: HTML (continued) and The Basics of CSS

---

# Announcements

- Reminder: [Problem Set 0](https://umich.instructure.com/courses/732026/assignments/2599400) due Sunday
- Office Hours (time TBA) will start **next week**
- Please **only** add `soney` as a collaborator in your `si379` repository.
  - An earlier version of the assignment inadvertently asked you to add two other Github accounts; please remove them
- If you haven't already, please pull out your laptop and [install Visual Studio Code](https://code.visualstudio.com/)

---
# Reading Paragraph

When you browse the web, what appears on your screen is actually the result of carefully structured content and styling working together. HTML creates the structure, like the skeleton of a building, while CSS applies the visual styling—the paint, decorations, and arrangement that make it visually appealing. 

HTML might seem simple at first glance, but it's the blueprint that browsers use to create what's called the Document Object Model (DOM)—a living, interactive representation of your webpage. HTML elements are like building blocks, each created with tags that wrap your content: `<tag>content</tag>`. These elements form a family tree with clear relationships: the `<html>` element serves as the root, containing `<head>` for invisible metadata and `<body>` for visible content. Within these containers, we use various semantic elements to give meaning to our content. Headings (`<h1>` through `<h6>`) establish importance hierarchy, paragraphs (`<p>`) contain text blocks, links (`<a>`) create connections between pages, images (`<img>`) display visual content, and buttons (`<button>`) enable interaction. Generic containers like `<div>` (for block sections) and `<span>` (for inline sections) help organize content when more specific semantic elements don't apply.

Elements gain extra powers through attributes—modifiers that provide additional information. For example, links need to know where they lead (`href`), images need their source (`src`) and descriptive text (`alt`), and any element can have `class` or `id` attributes that help us select them with CSS. 

CSS (Cascading Style Sheets) is our design toolkit for controlling how elements display. We can apply CSS in three ways: inline directly on elements using the `style` attribute, internally within a `<style>` tag in the document head, or externally in a separate file linked with `<link>`. CSS rules use selectors to target specific elements (like all paragraphs with `p { }`, elements with a specific class with `.className { }`, or a unique element with `#idName { }`), followed by properties and values that define the appearance.

When multiple CSS rules apply to the same element, the \"layered\" nature of CSS determines which rule wins—generally, more specific selectors take priority, with inline styles overriding all others. This behavior gives CSS tremendous flexibility but requires understanding its priority rules. Using semantic HTML—choosing elements based on their meaning rather than just their display—makes your page more accessible to screen readers and search engines. While you could make text look like a heading using CSS on a `<div>`, using an actual `<h1>` element communicates its semantic importance to browsers and assistive technologies.

The DOM—the browser's internal representation of your HTML—is what you see and interact with, while HTML is what you write to create it, and CSS is what you write to style it. Developer tools in browsers let you inspect this DOM and see how your code translates to what appears on screen. By understanding these foundational concepts, you're building the essential knowledge needed for creating well-structured, visually appealing web content.

---
# Recall...

- HTML elements are created with **tags**

![](images/element_illustration.png)

- Tags can contain **attributes**

```html
<tag attr1="value1" attr2="value2">content</tag>
```

- These elements form a **tree**

---

# Top-Level HTML Elements

- `<html>`: the document **root**
- `<head>`: document metadata (not visible)
- `<body>`: **visible** document content

```html
<!DOCTYPE html> <!-- Say that we're using HTML 5 --->
<html>
  <head> <!--    metadata     --> </head>
  <body> <!-- visible content --> </body>
</html>
```

---

# Other Common HTML Elements

* `<h1>`: Heading
* `<a>`: Link
* `<img>`: Image
* `<button>`: Button


---

# Exercise 1: Writing out HTML

- Create a directory named `lecture-02`
- Open VS Code and open the `lecture-02` directory
- Create a file named `index.html` in the `lecture-02` directory
- Add the following content (Note: `<a>` uses `href` to specify the link target):
![](images/basic_html_quiz.png)
- Open in a browser
  - Recommended plugin for VS Code: [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)

---

# Generic Containers

- `<div>`: Block section
- `<span>`: Inline section

![](images/div_vs_span.png)

---

# Semantic HTML

- HTML elements have [meaning](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html)
- Using the **correct** element helps make your page **understandable**
  - Typically for **screen readers** and **search engines**
  - Makes your code **more accessible** to people with disabilities
- For example, use `<h1>` for the **main heading** of a page

---

# Common Attributes

- `class` and `id` can be applied to any element

```html
<p class="selected">This is a selected paragraph</p>
<p id="footer">This is a paragraph in the footer</p>
```

* `class` and `id` will be used to **select** elements for styling
  (e.g., every element with `class="selected"` will be yellow)

---

# Essential HTML Elements for 379

```html
<!DOCTYPE html>                            <!-- Using HTML 5 -->
<html>                          <!-- Always the root element -->
  <head>                         <!-- Metadata (not visible) -->
    <title>My Page</title>
  </head>
  <body>                                <!-- Visible content -->
    <h1>My Page</h1>                             <!-- Header -->
    <a href="https://umich.edu">This is a link</a> <!-- Link -->
    <img src="..." />                             <!-- Image -->
    <button>Click me!</button>                   <!-- Button -->
    <div class="x">A block</div>          <!-- Block section -->
    <span id="y">An inline block</div>   <!-- Inline section -->
  </body>
</html>
```

---

# CSS

- **C**ascading **S**tyle **S**heets
- A language for describing how the browser should **display** elements

---

# Three ways to insert CSS:

1. **Inline**: directly in the HTML element
2. **Internal**: in a `<style>` element in the `<head>`
3. **External**: in a separate `.css` file

---

# Inline CSS (Method 1 to Insert CSS)

- Use the `style` attribute on an element

```html
<p style="color: red;">This is a red paragraph</p>
```

- The value of the `style` attribute is a **list of CSS declarations**
- Each declaration is a **property** and a **value**, separated by a colon
- Multiple declarations are separated by semicolons

---

# CSS Properties

- There are many CSS properties
- Each property has a set of **valid values**
- For example, the `color` property can be set to any [color name](https://developer.mozilla.org/en-US/docs/Web/CSS/named-color) or [hex code](https://developer.mozilla.org/en-US/docs/Web/CSS/hex-color)

```html
<p style="color: red;">This is a red paragraph</p>
<p style="color: #ff0000;">This is also a red paragraph</p>
```
---

# Internal CSS (Method 2 to Insert CSS)

- Use a `<style>` element in the `<head>` of the document
- Unlike "inline" style, we need to specify **which element(s)** using **selectors**

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      p {
        color: red;
      }
    </style>
  </head>
  <body>
    <p>This is a red paragraph</p>
  </body>
</html>
```

---

# CSS Selectors

- Say **which elements** a style applies to

* **Tag selector**: select all elements of a given tag
```css
p { color: red; } /* Applies to all paragraphs */
```
* **Class selector**: select all elements with a matching `class`
```css
.selected { color: red; } /* Applies to everything with the "selected" class */
```
* **ID selector**: select the element with a matching `id`
```css
#footer  { color: red; } /* Applies to the element with id "footer" */
```

---

# Exercise 2: Create the following CSS rules:
Update the `style` element in `index.html` to create the following rules:
![](images/styled_basic_html.png)

- The `body` element should have background color set to **black** and text color set to **white**
- `h1` elements should have text color set to **yellow**
- `a` elements should have no underline (`text-decoration: none;`) and text color set to `royalblue`

---

# "Cascading" Style Sheets

What happens if we have multiple styles that apply to the same element?

```html
<html>
  <head>
    <style>
      p {
        color: red;
      }
    </style>
  </head>
  <body>
    <p style="color: blue;">This is a blue paragraph</p>
  </body>
</html>
```

[Complex rules](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance#conflicting_rules) determine priority
Gross simplification: the **more specific** rule wins (and if not, the latest rule wins)



---

# External CSS (Method 3 to Insert CSS)

- Use a `<link>` element in the `<head>` of the document
- The `href` attribute specifies the **path to the CSS file**

```html
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <p>This is a red paragraph</p>
  </body>
</html>
```

`style.css`:
```css
p { color: red; }
```

---

# Essential HTML Elements for 379 (Added CSS)

```html
<!DOCTYPE html>                            <!-- Using HTML 5 -->
<html>                          <!-- Always the root element -->
  <head>                         <!-- Metadata (not visible) -->
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">  <!-- CSS Style -->
  </head>
  <body>                                <!-- Visible content -->
    <h1>My Page</h1>                             <!-- Header -->
    <p>This is a paragraph</p>                <!-- Paragraph -->
    <a href="https://umich.edu">This is a link</a> <!-- Link -->
    <img src="..." />                             <!-- Image -->
    <button>Click me!</button>                   <!-- Button -->
    <div class="x">Block</div>            <!-- Block section -->
    <span id="y">An inline block</div>   <!-- Inline section -->
  </body>
</html>
```

---

# Essential CSS for 379

## Selectors
```css
h1 { ... } /* Select all h1 elements */
#x { ... } /* Select the element with id "x" */
.x { ... } /* Select all elements with class "x" */
```

## Properties:

- `color`: text color
- `background-color`: background color
- `width` and `height`: (e.g., `width: 100px;`)

---

# Semantic HTML (Revisited)

* HTML elements have [meaning](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html)
* Using the **correct** element helps make your page **understandable**
  - Typically for **screen readers** and **search engines**
  - Makes your code **more accessible** to people with disabilities
* Can use **CSS** to style elements differently

---

Question: Given the choice between using CSS and HTML to style an element, which should you use?

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            .header {
                font-size: 2em;
                font-weight: bold;   
            }
        </style>
    </head>
    <body>
        <h1>This was styled using an h1</h1>
        <div class="header">This was styled using CSS</div>
    </body>
</html>
```

---

# Use the element that is **most semantically appropriate**

...but in 379, we won't mark you down for using generic `<div>` and `<span>` elements

---

# Combining Selectors

- We can combine selectors to create more specific rules
- For example, we can select all `<p>` elements with `class="selected"`

```css
p.selected { color: red; }
```

- We can also select all `<p>` elements **inside** a `<div>` with `class="x"`

```css
div.x p { color: red; }
```

---

What does the selector `#x` select?

1. All elements with `id="x"`
2. All elements with `class="x"`
3. All elements with `name="x"`
4. All elements with tag `x`

---

What does the selector `#x` select?

1. **All elements with `id="x"`**
2. All elements with `class="x"`
3. All elements with `name="x"`
4. All elements with tag `x`

---

What does the selector `div .highlighted` select?
(note the **space** between `div` and `.highlighted`)

1. All elements with `id="highlighted"` inside a `<div>`
2. All elements with `class="highlighted"` inside a `<div>`
3. All `<div>` elements with `class="highlighted"`
4. All `<div>` elements with `id="highlighted"`

---

What does the selector `div .highlighted` select?

1. All elements with `id="highlighted"` inside a `<div>`
2. **All elements with `class="highlighted"` inside a `<div>`**
3. All `<div>` elements with `class="highlighted"`
4. All `<div>` elements with `id="highlighted"`

---

What does the selector `div.highlighted` select?
(note **no space** between `div` and `.highlighted`)

1. All elements with `id="highlighted"` inside a `<div>`
2. All elements with `class="highlighted"` inside a `<div>`
3. All `<div>` elements with `class="highlighted"`
4. All `<div>` elements with `id="highlighted"`

---

What does the selector `div.highlighted` select?

1. All elements with `id="highlighted"` inside a `<div>`
2. All elements with `class="highlighted"` inside a `<div>`
**3. All `<div>` elements with `class="highlighted"`**
4. All `<div>` elements with `id="highlighted"`

---

# Exercise 3

- Create an HTML file named `exercise-3.html` and a CSS file named `exercise-3.css` in the `lecture-02` directory.
- In exercise-3.html, create the following HTML tree:

- `html`
  <!-- - `head`
    - `title`: "Exercise 3"
    - `link`: `rel="stylesheet"` and `href="exercise-3.css"` -->
  - `body`
    - `h1`: "Exercise 3"
    - `div`: `id="container"`
      - `p`: `class="highlighted"` "This is a paragraph"
      - `p`: "This is another paragraph"
    - `p`: `class="highlighted"` "This is a paragraph outside of container"
- ...continued on next page...

---

- Add a `<link>` element to the `<head>` of `exercise-3.html` to load `exercise-3.css`
- In exercise-3.css, create the following rules:
  - Any element with ID `container` should have a background color of `#CCC`
  - Any element with class `highlighted` should have a background color of `green`
  - Any element with class `highlighted` inside an element with ID `container` should have a background color of `yellow`

![](images/nested_css.png)

---

# The DOM (**D**ocument **O**bject **M**odel)

- The DOM is a **tree** that represents the structure of a web page
- The DOM is **dynamic** and **mutable**
    - We can **change** the DOM
    - We can **add** and **remove** elements
- When we write HTML, we are **creating** the DOM
* ...by the way, CSS creates the CSSOM....but no need to talk about that

---

# The DOM (**D**ocument **O**bject **M**odel)

![](images/dom_tree.png)

---

- The DOM is what we **see** and **interact with**
* HTML is what we write to **create** the DOM
* CSS is what we write to **style** the DOM
* JavaScript is what we write to **change** the DOM

---

![](images/DOM%20JS%20CSSOM.png)

---

# How do we see the DOM?

* Developer tools!
* Right click on a page and select "Inspect"

---

# Lecture 2 Handout

[Handout](https://umich.instructure.com/courses/732026/files/38943549?module_item_id=4142472)

---

# Problem Set 0
