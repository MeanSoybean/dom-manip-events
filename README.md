[Mozilla Reference on Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)

# DOM - Document Object Model

The DOM is a tree of nodes. The document is the root, each node is an element, and may parent other children nodes.

# NodeList vs Array of Nodes

As you use the Document API, you will encounter return objects such as the `Node` and `NodeList`.
The [`Node`](https://developer.mozilla.org/en-US/docs/Web/API/Node) class is an abstract class from which other DOM API classes are based, letting them be used similarly and often interchangeably. Notable Node subclasses include `Document`, `Element`, `DocumentFragment`.

The `NodeList` is not quite an array as some array methods are missing. Nonetheless you can convert it to one using `Array.from()` or the [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

# Find, Alter, Add, Remove Nodes

## Targeting Nodes with Selectors

The keyword `document` is a reference to the root of the DOM - the HTML document itself, i.e. the current loaded webpage.

You can use `element.querySelector(selectors)` to find the first descendant of the element that matches the selectors (provided as a string), or `element.querySelectorAll(selectors)` to receive a NodeList of all matches.

You can use _relational selectors_ such as `firstElementChild`, `lastElementChild`, `previousElementSibling` as well.

## Creating Nodes

`document.createElement(tagName, [options])` creates a new element of the tag type `tagName` and returns it for use **in memory**, and does not yet render it to the DOM. So you won't see any changes until you manually place the element into the DOM.

`parentNode.appendChild(childNode)` adds `childNode` to `parentNode` as the last child.

`parentNode.insertBefore(newNode, referenceNode)` inserts `newNode` as a child of `parentNode`, but before `referenceNode`.

## Removing Nodes

`parentNode.removeChild(childNode)` removes the child node and returns a reference to said node. Much like `pop` in common data structures.

## Altering Nodes

### Inline style

- `div.style.backgroundColor = 'blue'`
- `div.style.cssText = 'background-color: blue;';`
- `div.setAttribute('style', background-color: blue;);`
- `div.style['background-color'] = 'blue'`

### Editing attributes

- `element.setAttribute(attribute, value)` sets the attribute to the value
- `element.getAttribute(attribute)` returns the value of the attribute.
- `element.removeAttribute(attribute)` removes the specified attribute.

### Working with classes

- `element.classList.add(className)`
- `element.classList.remove(className)`
- `element.classList.toggle(className)` adds if the element doesn't have the class and returns true, or removes it and returns false if the element does have the class.

### Adding content

[Compare](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText#examples) `HTML.innerText` to `Node.textContent`.

Be careful about using [`innerHTML`](<https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML#usage_notes:~:text=Note%3A%20This%20is%20a%20security%20risk%20if%20the%20string%20to%20be%20inserted%20might%20contain%20potentially%20malicious%20content.%20When%20inserting%20user%2Dsupplied%20data%20you%20should%20always%20consider%20using%20Element.setHTML()%20instead%2C%20in%20order%20to%20sanitize%20the%20content%20before%20it%20is%20inserted.>). Use [`element.setHTML()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/setHTML) instead to sanitize the HTML.

# Events

We can _listen_ for events such as mouse hover, keypresses, clicking, etc., and _fire_ functions when those events happen.

- Specify function attributes directly on the HTML elements.
- Set properties of the form `on[eventType]` such as `onclick`, `onmousedown`, etc. on the DOM nodes using JavaScript
- Or, attach event listeners.

## Direct event attribute setting

```html
<button onclick="alert('Hello world')">Click Me</button>
```

JavaScript is now in HTML, violating separation of concern. Also it's ugly as hell. Also, we can't bind onclick to multiple functions this way.

## Setting event property

```html
<!-- html -->
<button id="btn">Click Me</button>
```

```javascript
// javascript
const btn = document.querySelector("#btn");
btn.onclick = () => alert("Hello World");
```

Separation of concern is now respected, but we still can't have multiple event listeners for multiple functions.

## Adding event listeners

```js
const btn = document.querySelector("#btn");
btn.addEventListener("click", () => {
  alert("Hello World");
});
```

This is the preferred way to do it. Events are listened to in JavaScript - functionality is stored in scripts, not HTML, where elements are declared.

### More on event listeners

[MDN web docs - Introduction to events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

By using `addEventListener(eventType, listener)`, you are either adding:

1. a **function**, or
2. an **object** that **implements** a **handleEvent()** function

to the list of event listeners for the specified `eventType`. The function or handleEvent()-implementing object is called the _event listener_ (that's why it is added to the list of event listeners).

> **Terminology**: Event listeners are also referred to, interchangeably, as event handlers. Rigorously speaking, "event listener" waits for the event to happen, and "event handler" is the actual code that does something when the event happens.

Repeatedly calling addEventListener for the same event and the same listener will not add it to the list a second time.

> **Caveat**: Note that different instances of anonymous functions with the same source code are NOT the same listeners.

> **Terminology**: The function passed to the `listener` parameter of `addEventListener(eventType, listener)` is known as a _callback function_ because it is being called back later when the event fires/happens.

The callback function has the same return value and parameter as the `handleEvent()` method; that is, it accepts as a single parameter the `Event` object describing the event that has occurred, and returns nothing.

# Bubbling
