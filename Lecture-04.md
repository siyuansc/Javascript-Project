---
marp: true
theme: default
paginate: true
---

# SI 379
## Building Interactive Applications

Lecture 4: Adding Event Listeners

---

# Announcements (1 of 2)

- Office Hours
    - Starting this week
    - Tried to accommodate different schedules (unable to fully)
    - **Tuesdays 1-1:45 pm:** In-person (North Quad 4381)
    - **Fridays 11am-1pm:** [Virtual (Zoom)](https://umich.zoom.us/j/99515386058)
    - **By appointment** [(email me at soney@umich.edu)](mailto:soney@umich.edu)
- Slack
    - Please email me if you aren't able to access [the course Slack channel (`si-379-w25`)](https://umich.enterprise.slack.com/archives/C0894TNAX7Z)
    - **Strongly recommended:** [Install the Slack app](https://slack.com/get) on your phone and laptop (do not use web app)

---

# Announcements (2 of 2)

- Video playlists on Canvas
- [**Problem set 1**](https://umich.instructure.com/courses/732026/assignments/2599401) is due Sunday (AoE)

---

# Recap: The DOM

- The **DOM** is **key**; it's what we see in the browser
- We build the (initial) **DOM** with HTML


---
```html
<html>
    <head>
        <title>My title</title>
    </head>
    <body>
        <a href="https://umich.edu/">My link</a>
        <h1>My header</h1>
    </body>
</html>
```
![](images/dom_tree.png)

---

# Recap: The DOM is important

- We write and manipulate **the DOM tree**
    - **HTML** creates the initial DOM tree
    - **JavaScript** can manipulate the DOM tree
    - **CSS** can style the DOM tree
* Developer tools let us see the DOM tree
    - Also lets us debug JavaScript
    - ...and lots of other important things

---

# Recap: Mixing in JavaScript

- Option 1: Inline JavaScript
* Option 2: Internal JavaScript
    - ```html
      <script>
         // ...
      </script>
      ```
* Option 3: External JavaScript
    - ```html
      <script src="script.js"></script>
      ```
    - `script.js`:
      ```js
      // ...
      ```


---

# Recap: Querying the DOM

- In JavaScript, we "reach into" the DOM to find elements
* We use `document.querySelector(...)` to do this
    - ...or `document.querySelectorAll(...)` to find multiple elements

---

# Recap: JavaScript Loading Order

- Browser runs JavaScript **as soon as it loads**
- Elements must have loaded before JavaScript runs

```html
<head>
    <link rel="stylesheet" href="style.css">
    <script>
        const p = document.querySelector('p'); // DOES NOT WORK
        p.innerText = 'Updated paragraph text';
    </script>
</head>
<body>
    <p>This is a paragraph</p>
</body>
```

---

# JavaScript Loading Order

- Browser runs JavaScript **as soon as it loads**
- Elements must have loaded before JavaScript runs

```html
<head>
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
```

---

# Functions in JavaScript

...many ways to define functions

```javascript
const add = (a, b) => {       // Arrow function with block body
    return a + b;
}
```

...believe it or not, there's many more...
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

# Timeout Function

- `setTimeout` is a function that takes a callback function and a time in milliseconds (1 second = 1000 milliseconds)
* After the time has passed, the callback function is called
* Example: `setTimeout(callback, 1000);`

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
    - First argument is the event name (e.g., `"click"`)
    - Second argument is the callback function

```javascript
element.addEventListener('click', callback);
```

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

# DOM Manipulation

- **DOM manipulation** is changing the content of the page
* Steps:
    * Get a DOM element with `document.querySelector(...)`
    * Manipulate its properties (e.g., set `.innerText = ...`)
    * Example:
        ```javascript
        const p = document.querySelector('p');
        let newText = 'New paragraph text';

        p.addEventListener('click', () => {
            p.innerText = newText;
        });
        ```


---

<!-- ![bg contain](images/lec_4_paper_ex.png)

--- -->

# Exercise 1 (Do on your own computers)

Write code that create a button with the number `0`. Every time the user clicks the button, that number should increment by 1.

![](images/button_click_counter.gif)

Strategy:
1. Create an HTML page with a `button` element
2. Create a `<script/>` element with JavaScript
3. In JavaScript, use `document.querySelector` to get the button
4. Create a variable `clickCount` to store the number of clicks
5. Add an event listener that sets `clickCount = clickCount + 1` and updates the button text (`btn.textContent = clickCount;`)

---

Sample solution:

```html
<button>0</button>
```

```javascript
const btn = document.querySelector("button");
let clickCount = 0;
btn.addEventListener("click", () => {
    clickCount++;
    btn.textContent = clickCount;
});
```

---

# DOM Manipulation: Class List

- `.classList.contains(...)` checks if an element has a class
- `.classList.add(...)` adds a class to an element
- `.classList.remove(...)` removes a class from an element

---

# Exercise 2 (Do on your own computers)

Create a box that changes color (toggles between two colors) **when you click on it**. Hint: use the `.classList` attribute to add and remove classes.

starter code:

```html
<style>
    #box {
        width: 250px;
        height: 250px;
    }
    .red  { background-color: red; }
    .blue { background-color: blue; }
</style>

<!--- ... --->

<div id="box"></div>
```

---

Sample solution:

```javascript
const box = document.querySelector("#box");
const toggleColor = () => {
    if(box.classList.contains("red")) {
        box.classList.remove("red");
        box.classList.add("blue");
    } else {
        box.classList.remove("blue");
        box.classList.add("red");
    }
};
box.addEventListener("click", toggleColor)
toggleColor();
```

---

# Exercise 3 (Do on your own computers)

Create a box that changes color (toggles between two colors) **every 2 seconds**.

starter code:

```html
<style>
    #box {
        width: 250px;
        height: 250px;
    }
    .red  { background-color: red; }
    .blue { background-color: blue; }
</style>

<!--- ... --->

<div id="box"></div>
```

---

Sample solution:

```javascript
const box = document.querySelector("#box");
const toggleColor = () => {
    if(box.classList.contains("red")) {
        box.classList.remove("red");
        box.classList.add("blue");
    } else {
        box.classList.remove("blue");
        box.classList.add("red");
    }
    setTimeout(toggleColor, 2000);
};
toggleColor();
```

---

# Problem set 1

Due **Sunday** at midnight (AoE)