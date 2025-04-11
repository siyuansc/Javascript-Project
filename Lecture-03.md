---
marp: true
theme: default
paginate: true
---

# SI 379
## Building Interactive Applications

Lecture 3: The DOM and JavaScript Basics

---

- Problem Set 0: turn in **Sunday**
  - Be sure to sign up for a **student account** on GitHub
  - Make your 379 repository *private*
- Problem Set 1 is posted, due next Sunday
  - Note: due next Sunday *Anywhere On Earth* (AoE) time

---
## Reading Paragraph

When we first explored the web, we focused on structure and style—HTML for structure and CSS for appearance. Now, it’s time to bring our pages to life with behavior, and that means diving into JavaScript. Think of HTML as the skeleton of your site, CSS as the skin and clothing, and JavaScript as the muscles—it lets your site move, react, and respond.

JavaScript may look familiar to Python users, but it behaves differently. It’s more permissive, often "guessing" what you meant instead of throwing errors. That flexibility can be powerful—but also dangerous. Where Python forces clarity, JavaScript allows ambiguity. Variables need to be declared using `let` or `const`, and semicolons mark the end of statements, though they’re technically optional.

To write JavaScript, we can include it inline (inside HTML elements), internally (within a `<script>` tag), or externally (in a separate `.js` file). The best practice is to use external scripts and load them with `<script src="script.js"></script>`, ideally with the `defer` attribute so the script runs only after the HTML finishes loading. If you try to access elements before they’re available in the DOM, your script will fail.

JavaScript gives us direct access to the DOM—the browser’s internal representation of the page. Using `document.querySelector()`, we can select and manipulate elements based on their tag name, ID, or class. We can change the content with `.innerText` or `.innerHTML`, and adjust styling by modifying `.classList`. These tools are the foundation of DOM manipulation.

Functions in JavaScript come in many forms, from traditional declarations to concise arrow functions. More importantly, functions are "first-class"—they can be passed around like any other variable. This enables one of the most important patterns in JavaScript: callback functions. We pass one function into another, and it gets called later—like with `setTimeout()` or `addEventListener()`.

Event listeners let us respond to user interactions. Want to do something when a button is clicked? Use `addEventListener('click', callback)`. That callback can then change the text, add a class, or trigger any behavior you like. Combined with DOM access and manipulation, this forms the backbone of interactive applications.

Through this lecture, we’re not just learning syntax. We're learning to think in terms of interaction. JavaScript turns a webpage from something static into something alive. And as we’ll see, the power of this language lies not just in what it can do alone, but in how it works with the structure of HTML and the style of CSS to create fully interactive experiences.

---

# Essential HTML Elements for 379

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
p.x { ... } /* Select all p elements with class "x" */
div p { ... } /* Select all p elements inside a div */
```

## Properties:

- `color`: text color
- `background-color`: background color
- `width` and `height`: (e.g., `width: 100px;`)

---

# Imagine building software...

* ...where you have to **support old features** forever
<!-- You just keep adding new features on top of older ones -->
* ...where you need to **support code that is decades old**

---

![bg contain right](images/mac_9.png)
- ...where you have to **support old features** forever
- ...where you need to **support code that is decades old**

---


![bg contain right](images/mac_combo.png)
- ...where you have to **support old features** forever
- ...where you need to **support code that is decades old**
* ...and the first version was implemented in **10 days**
* ...by **one person**
* Welcome to JavaScript!
* **"ECMAScript"** is the official name for the JavaScript language
* ...but we'll just call it JavaScript

<!-- You'll ask questions like "why are there like three alternative ways to open this app? -->
<!-- Why are there two trash cans and why does one look super old??? --->

---
<!-- Scoped style -->
<style scoped>
h1 {
  color: white;
}
</style>

![bg fill](images/platypus.jpg)
# JavaScript!

---

- HTML: structure and shape (skeleton)
- CSS: style and outward appearance (skin)
- **JavaScript**: behavior and interaction (muscles)

![bg contain right](images/js-body-analogy.png)

---

# Key Differences from Python

- (in general), JavaScript is **permissive** and **forgiving**
    - by contrast, Python throws errors for almost everything
* JavaScript "figures out" what to do with your code
    * Python will throw an error if it doesn't know what to do
* ...this is often not a good thing...

---

**Mixing in JavaScript**

- Option 1: Inline JavaScript
    * ```html
      <button onclick="alert('Hello!')">Click me!</button>
      ```
    * ...we will **avoid** this
* Option 2: Internal JavaScript
    * ```html
      <script>
         // ...
      </script>
      ```
* Option 3: External JavaScript
    * ```html
      <script src="script.js"></script>
      ```
    * `script.js`:
      ```js
      // ...
      ```

---

JavaScript:
```javascript
const arr = [1, 2, 3];
const to_add = 4;
const new_arr = arr + to_add;

console.log(new_arr.length); // 6
```

---

Python:
```python
arr = [1, 2, 3]
to_add = 4
new_arr = arr + to_add
# Imagine that you have lots of unrelated code here...
print(len(new_arr))
```

---

Another example:

```javascript
'Ba'+ + 'a'+'a'
```
* Output: `'BaNaNa'`
  * (because `+'a'` is `NaN`)

---


# Python vs. JavaScript

## Variables must be **declared** (use `let` or `const`)

Python:
```python
x = 10;
y = 20
x = x + y # Reassigning x
```

JavaScript
```javascript
let   x = 10;
const y = 20;
x = x + y; // Reassigning x
```

---

# Python vs. JavaScript

## Variables must be **declared** (use `let` or `const`)

- `let` allows you to **reassign** the variable
- `const` makes the variable a **constant** (cannot be reassigned)
    - ...but you can still **mutate** the variable

```javascript
const arr = [1, 2, 3];
arr.push(4); // .push() is like .append()
```

- `var` is an older way to declare variables
    - ...but it has some weird behavior so we won't use it

---

# Python vs. JavaScript

## Logging to the console

Python:
```python
print("Hello world!")
```

JavaScript:
```javascript
console.log("Hello world!");
```
(Note: you must have the "Console" tab open in Firefox Dev Tools to see the output)

---

# Exercise 1: Creating a JavaScript file

- Create a new directory anywhere (e.g., `lecture-03`)
- Create a file `index.html`
- Create a file `script.js`
  - Include `script.js` in `index.html`
  - Add a `console.log("Hello");` statement to `script.js`
- Open `index.html` in Firefox and make sure you see "Hello" in the console


---

# Python vs. JavaScript

## Code Blocks

Python:
```python
if cond:
  x += 1
  print('cond is true')
  print('this is still in the if block')
print('this is outside of the if block')
```

JavaScript:
```javascript
if(cond) {
  x += 1;
  console.log('cond is true');
  console.log('this is still in the if block');
}
console.log('this is outside of the if block');
```

---

# Python vs. JavaScript

## Semi-colons

Python:
```python
x = 1
y = 2
z = 3
```

JavaScript:
```javascript
const x = 1;
const y = 2;
const z = 3;
```

---

# Python vs. JavaScript

## Comments

Python:
```python
# This is a Python comment
```

JavaScript:
```javascript
// This is a JavaScript comment
/*
    This is a multi-line comment
    ...still in the comment
*/
```

---

**Accessing the DOM (from element type)**

HTML:
```html
<p>This is a paragraph</p>
```

JavaScript:
```javascript
const p = document.querySelector('p');
console.log(p.innerHTML); // "This is a paragraph"

// OR

const p_elements = document.getElementsByTagName('p');
const p = p_elements[0];
console.log(p.innerHTML); // "This is a paragraph"
```

CSS:
```css
p {
  color: red;
}
```

---

**Accessing the DOM (from element ID)**

HTML:
```html
<p id="x">This is a paragraph</p>
```

JavaScript:
```javascript
const p = document.querySelector('#x')
console.log(p.innerHTML); // "This is a paragraph"
// OR
const p = document.getElementById('x');
console.log(p.innerHTML); // "This is a paragraph"
```

CSS:
```css
#x {
  color: red;
}
```


---

**Accessing the DOM (from element class)**

HTML:
```html
<p class="x">This is a paragraph</p>
```

JavaScript:
```javascript
const p = document.querySelector('.x')
console.log(p.innerHTML); // "This is a paragraph"
// OR
const p_elements = document.getElementsByClassName('x');
const p = p_elements[0];
console.log(p.innerHTML); // "This is a paragraph"
```

CSS:
```css
.x {
  color: red;
}
```

---

# Accessing the DOM

- `document.querySelector()` returns the **first** element that matches the selector
- `document.querySelectorAll()` returns **all** elements that match the selector

- ...there are other (older) methods but we won't use them

---

# Accessing the DOM

- Whenever you need to get an element from the DOM, you will use `document.querySelector()`
- `document.querySelector()` is a *key* method. You will use it **a lot**.

---

# JavaScript Loading Order

- Browser runs JavaScript **as soon as it loads**
- This means that if you try to access an element that hasn't loaded yet, it won't work

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
    <script>
        const p = document.querySelector('p'); // DOES NOT WORK
        p.innerHTML = 'This is a new paragraph';
    </script>
  </head>
  <body>
    <h1>My Page</h1>
    <p>This is a paragraph</p>
  </body>
</html>
```

---

# JavaScript Loading Order

- Browser runs JavaScript **as soon as it loads**
- This means that if you try to access an element that hasn't loaded yet, it won't work

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>My Page</h1>
    <p>This is a paragraph</p>
    <script>
        const p = document.querySelector('p'); // WORKS
        p.innerHTML = 'This is a new paragraph';
    </script>
  </body>
</html>
```

---

# JavaScript Loading Order

- Can use `defer` to tell the browser to **wait** until the page loads to run the script
- Only works for **external** scripts

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
    <script defer src="script.js"></script>
  </head>
  <body>
    <h1>My Page</h1>
    <p>This is a paragraph</p>
  </body>
</html>
```

---

# Exercise 2: Accessing the DOM

- In `index.html`, add a `<p>` element with the text "This is a paragraph"
- In `script.js`, use `document.querySelector()` to get the `<p>` element and assign it to the variable `paragraph`
- Use `console.log(paragraph)` to log the DOM element to the console

---

# Changing the DOM

- We can **change** the DOM using JavaScript

```javascript
const p = document.querySelector('p');
p.innerHTML = 'This is a new paragraph';
```


---


DOM elements have many properties that you can manipulate, including:
  - `.innerHTML`: the HTML inside the element
  - `.innerText`: the text inside the element
  - `.classList`: which has methods:
    - `.classList.add()`: add a class
    - `.classList.remove()`: remove a class
    - `.classList.toggle()`: toggle a class

---

# Exercise 3: Changing the DOM

- Update `script.js` to change the text of the `<p>` element to "Updated paragraph"
  - After getting a DOM element, you can use `.innerText` to change the text inside the element
- When you do this, your paragraph should say "Updated paragraph" instead of "This is a paragraph"

---

# Essential JavaScript for 379

## Variables
```javascript
let x = 10;   // can be re-assigned
const y = 20; // cannot be re-assigned
```

## Logging to the console
```javascript
console.log("Hello world!");
```

```javascript
if(cond) {
    // ...
}
```

- `document.querySelector()` returns the **first** element that matches the selector
- `document.querySelectorAll()` returns **all** elements that match the selector

---

Remember: use `document.querySelector()` to get a DOM element

---

# Functions in JavaScript

...many ways to define functions

```javascript
function add(a, b) {          // Function declaration
    return a + b;             //   ("traditional")
}
```

```javascript
const add = function(a, b) {  // Anonymous function expression
    return a + b;
}
```

```javascript
const add = (a, b) => {       // Arrow function with block body
    return a + b;
}
```

```javascript
const add = (a, b) => a + b;  // Arrow function with concise body
```

...believe it or not, there's more...
<!-- const add = new Function('a', 'b', 'return a + b'); -->

---

...will mainly use arrow functions *for now*...

```javascript
const add = (a, b) => {
    const result = a + b;
    return result;
};
```

---

<style scoped>
code {
  color: red;
}
</style>

- Functions are **first-class objects** in JavaScript (like Python)
    - Functions can be passed as arguments to other functions (`!important`)
    - Functions can be returned from other functions

---

![bg contain](images/function_single_arg.png)

<!-- A function that takes one argument I'll represent like this --->

<!-- and remember that a function accepts any number of arguments but always has **one** return value -->

<!-- if nothing is returned, `undefined` gets returned (like None in Python) -->

---

![bg contain](images/function_two_args.png)

---

![bg contain](images/function_three_args.png)

---
<style scoped>
code {
  color: red;
}
</style>

# Callback Functions `!important`

* Pass one function into another
* Function will be "called back" later
    * ...when depends on the specifics of the function
* This is the "bread and butter" of JavaScript

---


let's run some code:

```javascript
const callback = () => {
    console.log("Callback called");
};

setTimeout(callback, 1000); // 1000 milliseconds: 1 second
```

<!-- load keynote --->

---

# Event Listeners

- **Event listeners** are callback functions
    - Called when an event occurs
    - Event listener is "listening" for the event
- Register an event listener with `addEventListener`
    - Call on any DOM element
    - First argument is the event name
    - Second argument is the callback function

---

# Event Listeners

HTML:
```html
<button id="my-button">Button</button>
```

JavaScript:
```javascript
const button = document.querySelector('#my-button');
const callback = (event) => {
    console.log('Button clicked');
};
button.addEventListener('click', callback);
```

---

HTML:
```html
<button id="my-button">Button</button>
```

JavaScript:
```javascript
const button = document.querySelector('#my-button');
const callback = (event) => {
    console.log('Button clicked');
};
button.addEventListener('click', callback);
```

![center](images/click_event_listener.png)

<!-- event listener presentation -->

---

```javascript
const button = document.querySelector('#my-button');
const callback = (event) => {
    console.log('Button clicked');
};
button.addEventListener('click', callback);
```

...leave the `callback` anonymous

```javascript
const button = document.querySelector('#my-button');
// no more callback variable
button.addEventListener('click', (event) => {
    console.log('Button clicked');
});
```

---

...so we can use event listeners to respond to user input...

...but now, how do we change the page?

---

# DOM Manipulation: Class List

- `.classList.contains(...)` checks if an element has a class
- `.classList.add(...)` adds a class to an element
- `.classList.remove(...)` removes a class from an element
