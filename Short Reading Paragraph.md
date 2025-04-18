### Lecture01

To build interactive applications, we first need a clear way to describe the structure of a webpage. HTML provides this structure. It tells the browser what kind of content it's dealing with—headings, paragraphs, links, images—and how that content is organized on the page. In this course, we won’t focus on HTML for long, but understanding its logic is necessary before we start working with JavaScript and more complex interactions.

HTML uses tags to mark different parts of a document, and those tags are often nested to form a tree-like structure. You’ll also see attributes, which add extra meaning to elements. Some are familiar, like `href` in a link or `src` in an image. Others, like `id`, `class`, or `disabled`, help control behavior and interaction. Even when an attribute doesn’t have a value, like `disabled`, its presence can still affect how the browser interprets the element.

This lecture also introduces a few basic rules: tags are case-insensitive, some can be self-closing, and every HTML page starts with a `<!DOCTYPE html>` declaration. While modern tools can generate HTML automatically, knowing how it works will help you debug, adjust, and build more intentional interfaces. HTML may be simple, but it's the foundation everything else depends on.

---

### Lecture02

Writing HTML gives you a way to describe the structure of a page—what belongs where, and how different pieces of content relate to one another. But structure alone doesn't tell the full story. If everything on a page is rendered with the same font, the same color, and the same spacing, users are left to guess what's important and what's interactive. A heading might carry semantic weight, but without any visual distinction, it blends into the background. This disconnect between meaning and appearance is where CSS steps in.

CSS is not just about making things “look better.” It’s a tool for reinforcing the information architecture that HTML begins. A properly structured page still needs contrast, rhythm, and spacing to communicate clearly. Consider a simple link: the HTML anchor tag gives it functionality, but it's CSS that gives it affordance—changing its color, removing the underline, or highlighting it on hover. These stylistic decisions carry cognitive weight. They help users scan content more efficiently, understand hierarchy, and act with confidence.

One of the most powerful aspects of CSS is that it separates design from structure. Instead of mixing presentation rules directly into the HTML, we can move styles into the `<style>` block or an external stylesheet. This makes our code easier to manage and reuse. Using selectors like `class`, `id`, or even combinations like `div p.selected`, we can target specific elements and define how they should appear in context. The “cascading” nature of CSS allows for flexible overrides and specificity, giving developers fine-grained control over visual behavior.

So while HTML lays the foundation—defining what elements exist and where they go—CSS adds the layer that makes interfaces understandable and usable. In that sense, structure and style aren’t separate stages of development, but parallel systems that work together to create meaning through both content and form.


---

### Lecture03

So far, HTML has given us structure, and CSS has helped shape its appearance. But a page that only displays content is still passive. Interactivity—the ability for a page to respond to user actions—is what brings modern interfaces to life. This is where JavaScript becomes essential. Unlike HTML and CSS, JavaScript isn’t about what’s on the page or how it looks—it’s about what happens when someone clicks, types, or scrolls.

JavaScript works by interacting with the DOM, the browser’s internal representation of a webpage. Through methods like `document.querySelector()`, we can select elements and read or modify them. For example, changing the text inside a paragraph, updating a class name, or even creating new elements entirely. Understanding how the DOM maps to HTML structure is key—every element in your HTML can be targeted and changed after the page loads.

The language itself differs from Python in both style and philosophy. JavaScript is more permissive, often running even when the code isn’t perfect. It uses `let` and `const` for variable declarations and requires explicit use of curly braces and semicolons. Though this flexibility allows for quick changes, it also makes debugging more subtle bugs important to learn early on.

One of the most important ideas introduced in this lecture is the **event listener**—a way to execute code in response to user actions. Using `addEventListener`, we can attach custom behavior to any HTML element. Combined with callback functions, this allows us to build programs that feel dynamic and responsive. A click can trigger a new message, a keypress can update a display, and form input can be validated in real time.

With JavaScript, the page is no longer just a document—it becomes an environment that reacts, changes, and communicates with the user. This shift from static content to interactive behavior marks a major turning point in building user interfaces.

---

### Lecture04
Building an interactive page means more than just displaying updated content—it means responding to what the user does. JavaScript allows us to observe those actions through *event listeners*, which are functions that run when something happens: a button is clicked, a key is pressed, or the mouse moves across the screen. Unlike the static DOM structure defined by HTML, event listeners create a two-way connection between the user and the browser.

Setting up an event listener follows a simple pattern: select an element, define a function, and register it with `addEventListener`. When that event occurs, your function is executed. This pattern is at the core of nearly every modern user interface. A button that counts clicks, a div that changes color, a text field that validates input—all of these are made possible by attaching small pieces of logic to specific user actions.

Because the browser reads and runs JavaScript as soon as it loads, timing also matters. We must make sure the elements exist in the DOM before we try to select them. This is why script tags are often placed at the bottom of the page, or loaded using `defer` in the `<head>` when external JavaScript files are used.

This lecture also emphasizes *DOM manipulation*—changing what’s displayed on the page in response to interaction. By combining `querySelector()` with methods like `.innerText`, `.classList.add()`, and `.classList.remove()`, we can alter both content and appearance in real time. Whether it's toggling a box's color or incrementing a counter, these changes are small, but they demonstrate the underlying power of JavaScript to turn static documents into living systems.

The result is a page that doesn't just sit and wait to be read—it listens, reacts, and evolves as the user engages with it. This kind of behavior is not an extra layer—it’s the heart of interactive application design.

---

### Lecture05
As event listeners become a regular part of our code, the logic behind how and when they run starts to matter more. It's not just about listening for a click—it’s about managing what should happen next, and under what conditions. In this lecture, we start to treat event handling as a pattern: using function objects, sometimes anonymous, and controlling their behavior with conditional logic, class manipulation, and timing.

The key to more dynamic interfaces lies in how we update the DOM. For example, toggling classes with `.classList.add()` and `.classList.remove()` allows us to reflect changes in visual state—like flipping a box from red to blue, or marking an element as “clicked.” These manipulations can be temporary, too, using functions like `setTimeout()` to automatically revert changes after a delay. Small design decisions like these make interfaces feel more responsive, even when the underlying action is simple.

But not all interactions involve a single element. As we scale up—from one image to many, or one button to a grid—we rely on `document.querySelectorAll()` and looping structures like `for...of` to apply listeners to multiple elements. This introduces a new layer of thinking: how to write code that’s not just correct once, but repeatable and modular.

Through these exercises, we see JavaScript shifting from a tool that simply reacts, to one that anticipates and manages interaction over time. The browser becomes not just a place to display content, but a system for receiving input, tracking state, and expressing logic visually through the DOM. It’s a shift from event handling as an action, to event handling as architecture.
