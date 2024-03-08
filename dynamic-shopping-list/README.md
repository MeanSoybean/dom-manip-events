# [Active learning: Dyanmic shopping list](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents#active_learning_a_dynamic_shopping_list)

In this challenge we want to make a simple shopping list example that allows you to dynamically add items to the list using a form input and button. When you add an item to the input and press the button:

- The item should appear in the list.
- Each item should be given a button that can be pressed to delete that item off the list.
- The input should be emptied and focused ready for you to enter another item.

1. To start with, download a copy of our shopping-list.html starting file and make a copy of it somewhere. You'll see that it has some minimal CSS, a div with a label, input, and button, and an empty list and `<script>` element. You'll be making all your additions inside the script.
1. Create three variables that hold references to the list (`<ul>`), `<input>`, and `<button>` elements.
1. Create a function that will run in response to the button being clicked.
1. Inside the function body, start off by storing the current value of the input element in a variable.
1. Next, empty the input element by setting its value to an empty string — ''.
1. Create three new elements — a list item (`<li>`), `<span>`, and `<button>`, and store them in variables.
1. Append the span and the button as children of the list item.
1. Set the text content of the span to the input element value you saved earlier, and the text content of the button to 'Delete'.
1. Append the list item as a child of the list.
1. Attach an event handler to the delete button so that, when clicked, it will delete the entire list item (`<li>`...`</li>`).
1. Finally, use the focus() method to focus the input element ready for entering the next shopping list item.
