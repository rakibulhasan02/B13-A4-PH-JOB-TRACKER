


## Answers to Questions

### 1. What is the difference between getElementById, getElementsByClassName, and querySelector / querySelectorAll?

Answer:
 getElementById: Selects a single element based on its unique id attribute;Returns the Element object if found; otherwise, returns null;The fastest selection method because the browser uses an internal lookup table for IDs.
getElementsByClassName: Selects all elements that possess the specified class name; Returns a Live HTMLCollection.Being "Live" means if the DOM updates (e.g., a new element with that class is added via JS), the collection updates automatically without re-running the command.
querySelector / querySelectorAll: Selects elements using standard CSS Selector syntax (e.g., '.class', '#id', 'div > p').querySelector: Returns only the first matching element. element.querySelectorAll: Returns all matching elements as a Static NodeList.

### 2. How do you create and insert a new element into the DOM?
Answer:
Here are the main ways to create and insert elements into the DOM:
Creating an element:
javascriptconst newElement = document.createElement('div');
newElement.textContent = 'Hello, World!';
newElement.classList.add('my-class');
Inserting into the DOM:
appendChild — adds to the end of a parent:
javascriptparentElement.appendChild(newElement);
insertBefore — inserts before a specific child:
javascriptparentElement.insertBefore(newElement, referenceElement);
prepend / append — modern, flexible methods that accept multiple nodes or strings:
javascriptparentElement.prepend(newElement);   // inserts at the beginning
parentElement.append(newElement);    // inserts at the end
insertAdjacentElement — most precise positioning control:
javascriptreferenceElement.insertAdjacentElement('beforebegin', newElement); // before the element
referenceElement.insertAdjacentElement('afterbegin', newElement); 
referenceElement.insertAdjacentElement('beforeend', newElement);   
referenceElement.insertAdjacentElement('afterend', newElement);  

### 3. What is Event Bubbling? And how does it work?
Answer:Event Bubbling is a concept in JavaScript where an event starts from the target element (the element that was clicked or triggered) and then bubbles up to its parent elements one by one until it reaches the top of the DOM (usually the document).
In simple words:
When you click a child element, the event also triggers on its parent, grandparent, and so on.
How Event Bubbling Works
Suppose we have this HTML:
<div id="parent">
    <button id="child">Click Me</button>
</div>
If we add event listeners:
document.getElementById("parent").addEventListener("click", function() {
    console.log("Parent clicked");
});
document.getElementById("child").addEventListener("click", function() {
    console.log("Child clicked");
});


### 4. What is Event Delegation in JavaScript? Why is it useful?
Answer:Event Delegation is a technique in JavaScript where you take advantage of Event Bubbling to handle events at a higher level in the DOM than the actual element where the event happened.Instead of attaching an event listener to every single child element, you attach one listener to their parent.
Gemini said
Event Delegation is a technique in JavaScript where you take advantage of Event Bubbling to handle events at a higher level in the DOM than the actual element where the event happened.

Instead of attaching an event listener to every single child element, you attach one listener to their parent.

How it Works
When a child element (like a button or list item) is clicked, the event "bubbles up" to its parent, then its grandparent, and so on. The parent can "catch" this event, figure out which child was clicked, and act accordingly.

Why is it Useful? (The Benefits)
Memory Efficiency: Attaching 1,000 listeners to 1,000 table rows uses a lot of memory and can slow down the browser. One listener on the <table> uses almost none.

Dynamic Elements: If you add a new row to a list via JavaScript after the page has loaded, it won't have a listener attached to it. With delegation, the parent is already listening, so the new item works immediately without extra code.

Cleaner Code: You have one central place to manage events for a group of elements.


### 5. What is the difference between preventDefault() and stopPropagation() methods?
preventDefault(): The messenger keeps walking up the stairs (bubbling), but he throws the letter away (the action doesn't happen).

stopPropagation(): The messenger performs the action but is tackled on the current floor; he cannot go up the stairs to the next level (the parents).

stopImmediatePropagation(): The messenger is tackled the moment he enters the room; he can't even talk to the other people standing in the same room (other listeners).


