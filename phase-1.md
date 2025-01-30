## Phase 1: Fundamentals (1-2 Months)
### Goal: Build a solid foundation in programming and web basics.

1. **Programming Basics with JavaScript (2-3 weeks)**
   - **Variables and Data Types**
     - var, let, const
     - Numbers, Strings, Booleans
     - null and undefined
     - Type conversion and coercion
     - **Code Sample:**
       ```javascript
       // Using let and const
       let age = 25;
       const name = "John Doe";

       // Type conversion
       let strAge = String(age);
       let numAge = Number(strAge);
       ```

   - **Operators**
     - Arithmetic operators (+, -, *, /, %)
     - Comparison operators (==, ===, !=, !==)
     - Logical operators (&&, ||, !)
     - Assignment operators
     - **Code Sample:**
       ```javascript
       // Arithmetic operators
       let sum = 10 + 5;
       let product = 10 * 5;

       // Comparison operators
       console.log(10 === "10"); // false
       console.log(10 == "10");  // true

       // Logical operators
       let isAdult = age >= 18 && age < 65;
       ```

   - **Control Flow**
     - if/else statements
     - switch statements
     - Loops (for, while, do-while)
     - break and continue
     - **Code Sample:**
       ```javascript
       // if/else statement
       if (age >= 18) {
         console.log("Adult");
       } else {
         console.log("Minor");
       }

       // for loop
       for (let i = 0; i < 5; i++) {
         console.log(i);
       }
       ```

   - **Functions**
     - Function declarations vs expressions
     - Arrow functions
     - Parameters and arguments
     - Return statements
     - Function scope
     - **Code Sample:**
       ```javascript
       // Function declaration
       function greet(name) {
         return `Hello, ${name}`;
       }

       // Arrow function
       const add = (a, b) => a + b;

       console.log(greet("Alice"));
       console.log(add(5, 3));
       ```

   - **Arrays and Objects**
     - Array methods (push, pop, shift, unshift)
     - Array iteration (map, filter, reduce)
     - Object properties and methods
     - Object destructuring
     - **Code Sample:**
       ```javascript
       // Array methods
       let fruits = ["apple", "banana"];
       fruits.push("orange");
       fruits.pop();

       // Array iteration
       let numbers = [1, 2, 3, 4];
       let doubled = numbers.map(num => num * 2);

       // Object destructuring
       let person = { name: "John", age: 30 };
       let { name, age } = person;
       ```

   - **Resources:**
     - FreeCodeCamp JavaScript Course
     - JavaScript.info
     - Codecademy JavaScript Track
     - MDN JavaScript Guide

2. **HTML Fundamentals (1 week)**
   - **Document Structure**
     - DOCTYPE declaration
     - HTML root element
     - Head and body sections
     - **Code Sample:**
       ```html
       <!DOCTYPE html>
       <html lang="en">
       <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Document</title>
       </head>
       <body>
         <!-- Content goes here -->
       </body>
       </html>
       ```

   - **Essential Elements**
     - Headings (h1-h6)
     - Paragraphs (p)
     - Lists (ul, ol, li)
     - Links (a)
     - Images (img)
     - **Code Sample:**
       ```html
       <h1>Main Heading</h1>
       <p>This is a paragraph.</p>
       <ul>
         <li>List item 1</li>
         <li>List item 2</li>
       </ul>
       <a href="https://example.com">Example Link</a>
       <img src="image.jpg" alt="Description of image">
       ```

   - **Semantic HTML**
     - header, nav, main, article
     - section, aside, footer
     - figure and figcaption
     - **Code Sample:**
       ```html
       <header>
         <nav>
           <!-- Navigation links -->
         </nav>
       </header>
       <main>
         <article>
           <section>
             <h2>Section Heading</h2>
             <p>Section content...</p>
           </section>
           <aside>
             <p>Related content...</p>
           </aside>
         </article>
       </main>
       <footer>
         <p>Footer content...</p>
       </footer>
       ```

   - **Forms**
     - Input types (text, email, password)
     - Select dropdowns
     - Radio buttons and checkboxes
     - Form validation
     - **Code Sample:**
       ```html
       <form>
         <label for="name">Name:</label>
         <input type="text" id="name" name="name">
         
         <label for="email">Email:</label>
         <input type="email" id="email" name="email">
         
         <label for="password">Password:</label>
         <input type="password" id="password" name="password">
         
         <label for="gender">Gender:</label>
         <input type="radio" id="male" name="gender" value="male">
         <label for="male">Male</label>
         <input type="radio" id="female" name="gender" value="female">
         <label for="female">Female</label>
         
         <label for="hobbies">Hobbies:</label>
         <input type="checkbox" id="reading" name="hobbies" value="reading">
         <label for="reading">Reading</label>
         <input type="checkbox" id="traveling" name="hobbies" value="traveling">
         <label for="traveling">Traveling</label>
         
         <label for="country">Country:</label>
         <select id="country" name="country">
           <option value="usa">USA</option>
           <option value="canada">Canada</option>
         </select>
         
         <button type="submit">Submit</button>
       </form>
       ```

   - **Tables**
     - Table structure (table, tr, td, th)
     - Column and row spans
     - Table sections (thead, tbody, tfoot)
     - **Code Sample:**
       ```html
       <table>
         <thead>
           <tr>
             <th>Name</th>
             <th>Age</th>
           </tr>
         </thead>
         <tbody>
           <tr>
             <td>John</td>
             <td>30</td>
           </tr>
           <tr>
             <td>Jane</td>
             <td>25</td>
           </tr>
         </tbody>
         <tfoot>
           <tr>
             <td colspan="2">Footer content</td>
           </tr>
         </tfoot>
       </table>
       ```

   - **Resources:**
     - MDN HTML Guide
     - W3Schools HTML Tutorial
     - HTML.com

3. **CSS Fundamentals (1 week)**
   - **Selectors**
     - Element, class, and ID selectors
     - Attribute selectors
     - Pseudo-classes and pseudo-elements
     - Combinators
     - **Code Sample:**
       ```css
       /* Element selector */
       p {
         color: blue;
       }

       /* Class selector */
       .container {
         max-width: 1200px;
         margin: 0 auto;
       }

       /* ID selector */
       #header {
         background-color: #f8f9fa;
       }

       /* Attribute selector */
       input[type="text"] {
         border: 1px solid #ccc;
       }

       /* Pseudo-class */
       a:hover {
         color: red;
       }

       /* Pseudo-element */
       p::first-line {
         font-weight: bold;
       }

       /* Combinator */
       .nav ul > li {
         list-style: none;
       }
       ```

   - **Box Model**
     - Margin, padding, border
     - Width and height
     - Box-sizing property
     - **Code Sample:**
       ```css
       .box {
         width: 100px;
         height: 100px;
         padding: 10px;
         margin: 20px;
         border: 1px solid #000;
         box-sizing: border-box;
       }
       ```

   - **Layout**
     - Display property
     - Position (relative, absolute, fixed)
     - Flexbox
       - flex-direction
       - justify-content
       - align-items
       - flex-wrap
     - Grid
       - grid-template-columns/rows
       - grid-gap
       - grid-areas
     - **Code Sample:**
       ```css
       /* Flexbox */
       .flex-container {
         display: flex;
         flex-direction: row;
         justify-content: center;
         align-items: center;
         flex-wrap: wrap;
       }

       /* Grid */
       .grid-container {
         display: grid;
         grid-template-columns: repeat(3, 1fr);
         grid-gap: 10px;
         grid-template-areas:
           "header header header"
           "sidebar main main"
           "footer footer footer";
       }
       ```

   - **Responsive Design**
     - Media queries
     - Mobile-first approach
     - Viewport meta tag
     - Responsive units (%, vw, vh, rem, em)
     - **Code Sample:**
       ```css
       /* Media query */
       @media (max-width: 600px) {
         .container {
           flex-direction: column;
         }
       }

       /* Viewport meta tag (to be included in HTML) */
       <meta name="viewport" content="width=device-width, initial-scale=1.0">

       /* Responsive units */
       .responsive-text {
         font-size: 2rem; /* 2 * root element's font size */
       }
       ```

   - **Resources:**
     - CSS-Tricks
     - MDN CSS Guide
     - Flexbox Froggy
     - Grid Garden

4. **JavaScript DOM Manipulation (1 week)**
   - **Selecting Elements**
     - getElementById
     - querySelector/querySelectorAll
     - getElementsByClassName
     - getElementsByTagName
     - **Code Sample:**
       ```javascript
       // Selecting elements
       const header = document.getElementById('header');
       const items = document.querySelectorAll('.item');
       const listItems = document.getElementsByClassName('list-item');
       const paragraphs = document.getElementsByTagName('p');
       ```

   - **Modifying Elements**
     - innerHTML vs textContent
     - setAttribute/getAttribute
     - classList operations
     - style modifications
     - **Code Sample:**
       ```javascript
       // Modifying elements
       header.textContent = 'New Header Text';
       items[0].setAttribute('data-id', '123');
       items[0].classList.add('active');
       items[0].style.color = 'blue';
       ```

   - **Event Handling**
     - addEventListener
     - Common events (click, submit, load)
     - Event object properties
     - Event bubbling and capturing
     - **Code Sample:**
       ```javascript
       // Event handling
       header.addEventListener('click', (event) => {
         console.log('Header clicked', event);
       });

       document.querySelector('form').addEventListener('submit', (event) => {
         event.preventDefault();
         console.log('Form submitted');
       });
       ```

   - **DOM Traversal**
     - parentElement
     - children
     - nextSibling/previousSibling
     - **Code Sample:**
       ```javascript
       // DOM traversal
       const parent = items[0].parentElement;
       const firstChild = parent.children[0];
       const nextSibling = firstChild.nextSibling;
       const previousSibling = firstChild.previousSibling;
       ```

   - **Resources:**
     - JavaScript30 by Wes Bos
     - MDN DOM Manipulation Guide
     - W3Schools DOM Tutorial

5. **Mini Projects (1 week)**
   Build these projects combining all learned concepts:
   - **Interactive Form Validator**
     - Real-time validation
     - Error messages
     - Success states
   
   - **Todo List**
     - Add/remove items
     - Mark as complete
     - Local storage
   
   - **Simple Calculator**
     - Basic operations
     - Clear functionality
     - Keyboard support

   - **Image Gallery**
     - Grid layout
     - Lightbox feature
     - Responsive design

---