
### The DOM Programming Interface

The HTML DOM can be accessed with JavaScript.
In the DOM, all HTML elements are defined as **objects**.

The programming interface is the properties and methods of each object.

A **property** is a value that you can get or set (like changing the content of an HTML element). {eg. `.value`, `.innerText`, `.classList`}
A **method** is an action you can do (like add or deleting an HTML element).  {eg.
`getElementById()`, `.focus()`, `.click()`, `.setSelectionRange()`, `.appendChild()`}

(browser provides functionalities to JS with window obj)
window -> document -> HTML
The document object represents your web page.
If you want to access any element in an HTML page, you always start with accessing the document object.

