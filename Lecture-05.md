---
marp: true
theme: default
paginate: true
---

# SI 379
## Building Interactive Applications

Lecture 5: Practice with Event Listeners

---

# Announcements

- Introduction: Brann Khattiyanont (IA)
- Reminder Problem Set 1

---

# From Last time: Defining Functions


```javascript
const add = (a, b) => {       // Arrow function with block body
    return a + b;
}
```

- Defines `add` as a function that takes two arguments `a` and `b` and returns their sum.
* `add` is a **function object** (![height:50px](images/function_object.png))

---

# From Last Time: Event Listeners

- Write **event listeners** to respond to user actions
    - `element.addEventListener(eventType, callback)`
    - `callback` is a **function object** (![height:50px](images/function_object.png))

```javascript
const onTimeout = () => {
    console.log("One second passed");
}
setTimeout(onTimeout, 1000);

const onClick = () => {
    console.log("Clicked on element");
};
element.addEventListener("click", onClick);
```

---

# Function Objects

```javascript
const onTimeout = () => {
    console.log("One second passed");
}
setTimeout(onTimeout, 1000);
```
* What happens if we add parentheses to `onTimeout`?
    ```javascript
    setTimeout(onTimeout(), 1000);
    ```
    * `onTimeout` is **called** immediately and the return value (nothing) is passed to `setTimeout`
* It is important that the callback (e.g., `onTimeout` is a function **object** (![height:50px](images/function_object.png)).


---

# Anonymous Functions

```javascript
const callback = () => {
    console.log('Button clicked');
};
button.addEventListener('click', callback);
```

...we can also leave the `callback` anonymous:

```javascript
// no more callback variable
button.addEventListener('click', () => {
    console.log('Button clicked');
});
```

---

# From Before: DOM Manipulation

- Manipulate **the DOM** in JavaScript
    - Get a DOM element with `document.querySelector(...)`
    - Manipulate its properties (e.g., set `.innerText = ...`)
* Get an element by its `id` attribute (example: getting an element with ID `main-pic`):
    ```javascript
    const element = document.querySelector("#main-pic");
    ```

---

<!-- # Exercise From Last Lecture -->

**Exercise from last lecture:** Create a box that changes color (toggles between two colors) *when you click on it*. Hint: use the `.classList` attribute to add and remove classes.

- `el.classList.add("x");` **adds** class `x` to `el`
- `el.classList.remove("x");` **removes** class `x` from `el`
- `el.classList.contains("x");` **checks** if `el` has class `x`

<!-- starter code: -->

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

**Exercise 1 (Handout):** None of the following work. Why?

![width:850px](images/callback_problems_exercise.png)

---

# Getting Set Up with Git (on your own computers)

- Create a new repository on Github (done in PS 0)
- Get the URL of the repository (should end with `.git`)
    - `git@github.com:user...` *or* `https://github.com/user/repo.git`
    - is **NOT** the URL of the repository's page
![](images/github-repo-url.png)
- In VS Code click the "Source Control" icon ![](images/source_control_icon.png)
- Select "Clone Repository" and paste in the URL ![](images/clone_repository_button.png)
- Select a destination (where the code will be stored on **your** computer)
    - Remember where this is `!important`
    - Whenever working on 379 code, do it in this directory
    - Create a new sub-directory for each assignment

---

# Exercise 2 (Do on your own computers)

1. Download all the files from [Canvas -> Files -> Lecture Handouts -> Lecture 05 - Click Pow](https://umich.instructure.com/courses/732026/files/folder/Lecture%20Handouts/Lecture%2005%20-%20Click%20Pow) to your 379 repository (wherever you put it).
2. Edit `script.js` so that when the user clicks the "zzz" image, it changes to the "pow" image. Test using `click_pow.html` (**not** `multi_click_pow.html`).
    - When the user clicks the "pow" image, add the `"clicked"` class if it does not already have it.
    - Then, one second later, remove the `"clicked"` class

![](images/click_pow.gif)

---

Sample solution:

```javascript
const clickableElement = document.querySelector('#clickable_elem');

clickableElement.addEventListener('click', () => {
    if(!clickableElement.classList.contains('clicked')) {
        clickableElement.classList.add('clicked');
        setTimeout(() => {
            clickableElement.classList.remove('clicked');
        }, 1000);
    }
});
```

 
---

# Exercise 3: Syncing your code to Github (1 of 2)

- In VS Code click the "Source Control" icon ![](images/source_control_icon.png)
- Make sure your latest changes appear under "changes"
- Enter a commit message (e.g., "Add exercise 2 code")
- Click "Commit and Sync"
![](images/commit_and_sync.png)

---
# Exercise 3: Syncing your code to Github (2 of 2)
- If you get the message below, click "yes"
![](images/no-staged-changes.png)
- Check on Github that your code is there

---

# Exercise 4: Deploying to Github Pages (1 of 2)

- Go to the repository's settings page
- Scroll down to the "Pages" section
![](images/gh_pages_section.png)
- Select "Deploy fom Branch" under "Source"
- Select "main" as the branch and "/ (root)"; click "Save"
![](images/gh_pages_config.png)



---

# Exercise 4: Deploying to Github Pages (2 of 2)

- Look for "Your site is live at..." in the "Pages" section
![](images/site_live_at.png)
- Click on the link and **add to the URL** the path to the page you want:
  - `https://user.github.io/repo/` **+** `lectures/lecture-05/ex_1.html`
  - `https://user.github.io/repo/lectures/lecture-05/ex_1.html`
- Try this for the exercise (or really any code)
- Will do this for Problem Set 1
- Practice with ["Lecture 05" assignment in Canvas](https://umich.instructure.com/courses/732026/assignments/2599396)

---

# Three different `for` loops


Looping over lists/arrays:
```javascript
const arr = [10, 20, 30];
for(const num of arr) {
    // num is 10, then 20, then 30
}
```

Looping over dictionaries/objects:
```javascript
const obj = {'a': 10, 'b': 20, 'c': 30};
for(const key in obj) {
    // key is 'a', then 'b', then 'c'
}
```

---

# Three different `for` loops

"Traditional": Syntactic sugar for a `while` loop
```javascript
for(let i = 0; i < 5; i++) {
    console.log(i); // i is 0, then 1, then 2, then 3, then 4
}
```

---

# Exercise 5 (Do on your own computers)

- The file `multi_click_pow.html` is similar to `click_pow.html`, but it has many "pow" images instead of one.
- Update your code so that when the user clicks on any of the "pow" images, it changes to the "zzz" image.
    - Hint: use `document.querySelectorAll()` and a `for` loop

![height:300px](images/multi_click_pow.gif)

---

Sample solution:

```javascript
const clickableElements = document.querySelectorAll('.clickable');

for(const clickableElement of clickableElements) {
    clickableElement.addEventListener('click', () => {
        if(!clickableElement.classList.contains('clicked')) {
            clickableElement.classList.add('clicked');
            setTimeout(() => {
                clickableElement.classList.remove('clicked');
            }, 1000);
        }
    });
}
```

---

# Exercise 6: Sync updated code to Github

- In VS Code click the "Source Control" icon ![](images/source_control_icon.png)
- Make sure your latest changes appear under "changes"
- Enter a commit message (e.g., "Add exercise 2 code")
- Click "Commit and Sync"
![](images/commit_and_sync.png)
- **Check that your latest changes are deployed to Github Pages**

---

# Problem Set 1

- Due Sunday
- Demo: https://soney.github.io/si379-assignments/ps1/
![](images/problem_set_1.png)

---

# Problem Set 1: Code Review

- There are **two** places to write code. Both are marked with `console.log("TODO...")`
    1. Code inside of a call to `setInterval`:
        ```js
        const interval = setInterval(() => {
            console.log('TODO: Add the "needs-whack" class to a random hole');
        }, 1000);
        ```
        Note: `setInterval` runs the code inside of it every second
    2. Code inside of a `for` loop:
        ```js
        for(const id of getAllHoleIds()) {
            console.log(`TODO: Add a click listener for #${id} here`);
        }
        ```
---

# (if time) Work on Problem Set 1

- Due Sunday