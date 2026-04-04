```dataviewjs
const tasks = dv.current().file.tasks;
const total = tasks.length;
const done = tasks.where(t => t.completed).length;
const progress = total > 0 ? Math.round((done / total) * 100) : 0;

dv.paragraph(`**JavaScript Progress • ${done}/${total} (${progress}%)**`);

const barHtml = `
<div style="
  background: #f0f0f0;
  height: 24px;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
  margin: 10px 0;">
  <div style="
    height: 100%;
    width: ${progress}%;
    background: linear-gradient(to right, #667eea, #764ba2);
    border-radius: 12px;
    box-shadow: 0 0 10px rgba(102, 126, 234, 0.5);
    transition: width 0.6s ease;">
  </div>
</div>`;

dv.el("div", barHtml);
```
## 1️⃣ JavaScript Basics & Environment
- [x] What is JavaScript
- [x] What JavaScript can do
- [x] How to study JavaScript
- [x] Required tools & setup
- [x] Chrome Developer Tools
- [x] Where to write JavaScript code
- [x] Comments & bad practices
- [x] Output to screen
- [x] Console methods & styling
- [x] Web APIs overview
- [x] ECMAScript (ES)

## 2️⃣ Data Types & Variables
- [x] JavaScript data types
- [x] typeof operator
- [x] Variables introduction
- [x] Identifier naming rules
- [x] var vs let vs const
- [x] Type coercion

## 3️⃣ Strings
- [x] String syntax
- [x] Escape sequences
- [x] String concatenation
- [x] Template literals
- [x] String methods
- [x] String challenges

## 4️⃣ Numbers & Math
- [x] Numbers in JavaScript
- [x] Number methods
- [x] Math object
- [x] Arithmetic operators
- [x] Unary plus & negation
- [x] Assignment operators
- [x] Number challenges

## 5️⃣ Operators & Conditions
- [x] Comparison operators
- [x] Logical operators
- [x] Nullish coalescing operator
- [x] If / Else conditions
- [x] Nested if conditions
- [x] Ternary operator
- [x] Switch statement
- [x] Conditions challenges

## 6️⃣ Arrays
- [x] Array introduction
- [x] Array length
- [x] Add & remove elements
- [x] Sorting arrays
- [x] Slicing arrays
- [x] Joining arrays
- [x] Array challenges ✅ 2026-01-06

## 7️⃣ Loops
- [x] for loop
- [x] Looping over sequences
- [x] Nested loops
- [x] Break, continue & labels
- [x] Advanced loop examples
- [x] while loop
- [x] do...while loop
- [x] Loop challenges
- [x] Practical loop projects

## 8️⃣ Functions
- [x] Function basics
- [x] Advanced function examples
- [x] Return statement
- [x] Default parameters
- [x] Rest parameters
- [x] Anonymous functions
- [x] Arrow functions
- [x] Nested functions
- [x] Function challenges

## 9️⃣ Scope
- [x] Global scope
- [x] Local scope
- [x] Block scope
- [x] Lexical scope

## 🔟 Higher-Order Functions
- [x] map()
- [x] filter()
- [x] reduce()
- [x] forEach()
- [x] Higher-order function challenges

## 1️⃣1️⃣ Objects
- [x] Object introduction
- [x] Dot vs bracket notation
- [x] Nested objects
- [x] this keyword
- [x] Constructor functions
- [x] new keyword
- [x] Object.create()
- [ ] Object.assign()

## 1️⃣2️⃣ DOM (Document Object Model)
- [x] What is DOM
- [x] Select elements
- [x] Get & set content
- [x] Get & set attributes
- [x] Check attributes
- [x] Create & append elements
- [x] Deal with children
- [x] DOM events
- [x] Form validation
- [x] Event simulation
- [x] ClassList methods
- [x] Styling with JS
- [x] Insert & remove elements
- [x] DOM traversing
- [x] DOM cloning
- [x] addEventListener()
- [ ] DOM challenges

## 1️⃣3️⃣ BOM (Browser Object Model)
#### Topics
- [x] What is BOM ✅ 2025-12-22
- [x] Alert, confirm, prompt ✅ 2025-12-22
- [x] setTimeout & clearTimeout ✅ 2025-12-22
- [x] setInterval & clearInterval ✅ 2025-12-22
- [x] window.location ✅ 2025-12-22
- [x] Window open & close ✅ 2025-12-22
- [x] Window history ✅ 2025-12-22
- [x] Scroll methods ✅ 2025-12-22
- [x] Focus, print, stop ✅ 2025-12-22
- [x] Local Storage ✅ 2025-12-23
- [x] Session Storage ✅ 2025-12-23
- [x] BOM challenges ✅ 2025-12-23
#### Assignments
- [x] [From 102 to 110](https://elzero.org/javascript-bootcamp-assignments-lesson-from-102-to-110/) ✅ 2025-12-23 -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]]
- [x] [From 111 to 114](https://elzero.org/javascript-bootcamp-assignments-lesson-from-111-to-114/) ✅ 2025-12-23 -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]]
---
## 1️⃣4️⃣ Destructuring & Spread
#### Topics
- [x] Array destructuring ✅ 2025-12-24
- [x] Object destructuring ✅ 2025-12-24
- [x] Function parameters destructuring ✅ 2025-12-24
- [x] Swap variables ✅ 2025-12-24
- [x] Mixed destructuring ✅ 2025-12-24
- [x] Spread syntax ✅ 2025-12-24

#### Asignments
- [x] [From 115 to 122](https://elzero.org/javascript-bootcamp-assignments-lesson-from-115-to-122/) ✅ 2025-12-24 -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]]
---
## 1️⃣5️⃣ Advanced Data Structures
- [x] Set ✅ 2025-12-25
- [x] WeakSet ✅ 2025-12-25
- [x] Map ✅ 2025-12-25
- [x] Map methods ✅ 2025-12-26
- [x] WeakMap ✅ 2025-12-26
- [x] Array.from() ✅ 2025-12-26
- [x] copyWithin() ✅ 2025-12-26
- [x] some() ✅ 2025-12-26
- [x] every() ✅ 2025-12-26
- [x] Data structure challenges ✅ 2025-12-26
#### Asignments
- [x] [From 123 to 133](https://elzero.org/javascript-bootcamp-assignments-lesson-from-123-to-133/) ✅ 2025-12-24 -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2025-12-26

## 1️⃣6️⃣ Regular Expressions (Regex)
- [x] Regex basics ✅ 2025-12-28
- [x] Modifiers ✅ 2025-12-28
- [x] Ranges ✅ 2025-12-28
- [x] Character classes ✅ 2025-12-28
- [x] Quantifiers ✅ 2025-12-28
- [x] Replace patterns ✅ 2025-12-28
- [x] Form validation ✅ 2025-12-28
- [x] Regex challenges ✅ 2025-12-28
#### Assignments
- [x] [From 134 to 146](https://elzero.org/javascript-bootcamp-assignments-lesson-from-134-to-146/)  -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2025-12-29
 ---
## 1️⃣7️⃣ Object-Oriented Programming (OOP)
- [x] OOP principles ✅ 2025-12-29
- [x] Constructor functions ✅ 2025-12-29
- [x] Classes ✅ 2025-12-29
- [x] Static properties & methods ✅ 2025-12-29
- [x] Inheritance ✅ 2025-12-29
- [x] Encapsulation ✅ 2025-12-29
- [x] Prototypes ✅ 2025-12-29
- [x] Prototype chain ✅ 2025-12-29
- [x] Object descriptors ✅ 2025-12-29
#### Assignments
- [x] [From 147 to 158](https://elzero.org/javascript-bootcamp-assignments-lesson-from-147-to-158/) -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2025-12-29
---
## 1️⃣8️⃣ Date, Time & Generators
- [x] Date & time basics ✅ 2026-01-06
- [x] Get date & time ✅ 2026-01-06
- [x] Set date & time ✅ 2026-01-06
- [x] Formatting date ✅ 2026-01-06
- [x] Track execution time ✅ 2026-01-06
- [x] Generator functions ✅ 2026-01-06
- [x] Delegate generators ✅ 2026-01-06
- [x] Infinite generators ✅ 2026-01-06
#### Assignments
- [x] [From 159 to 168](https://elzero.org/javascript-bootcamp-assignments-lesson-from-159-to-168/)  -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2026-01-06
---
## 1️⃣9️⃣ Modules
- [x] ES Modules ✅ 2026-01-06
- [x] Import & export ✅ 2026-01-06
- [x] Named vs default exports ✅ 2026-01-06
#### Assignments
- [x] [From 159 to 168](https://elzero.org/javascript-bootcamp-assignments-lesson-from-159-to-168/)  -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2026-01-06
---

## 2️⃣0️⃣ JSON, AJAX & APIs
- [x] What Is JSON ✅ 2026-01-07
- [x] JSON Syntax And Compare With JS Object ✅ 2026-01-07
- [x] What Is API ✅ 2026-01-07
- [x] Parse And Stringify ✅ 2026-01-07
- [x] Asynchronous vs Synchronous Programming ✅ 2026-01-07
- [x] Call Stack And Web API ✅ 2026-01-07
- [x] Event Loop And Callback Queue ✅ 2026-01-07
- [x] What Is AJAX And Network Informations ✅ 2026-01-07
- [x] Request and Response From Real API ✅ 2026-01-07
- [x] Loop On Data ✅ 2026-01-07
#### Assignments
- [x] [From 169 to 178](https://elzero.org/javascript-bootcamp-assignments-lesson-from-169-to-178/)  -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2026-01-07
---

## 2️⃣1️⃣ Promises & Async/Await
 - [x] Callback Hell Or Pyramid Of Doom ✅ 2026-01-08
 - [x] Promise Intro And Syntax ✅ 2026-01-08
 - [x] Promise – Then, Catch And Finally ✅ 2026-01-08
 - [x] Promise And XHR ✅ 2026-01-08
 - [x] Fetch API ✅ 2026-01-08
 - [x] Promise – All, All Settled And Race ✅ 2026-01-08
 - [x] Async And Trainings ✅ 2026-01-08
 - [x] Await And Trainings ✅ 2026-01-08
 - [x] Try, Catch, Finally With Fetch ✅ 2026-01-08
 - [x] The End And Advices ✅ 2026-01-08
#### Assignments
- [x] [From 179 to 188](https://elzero.org/javascript-bootcamp-assignments-lesson-from-179-to-188/)  -> [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]] ✅ 2026-01-08
---

## Links
- [[learning/01_frontend/javascript/01_concepts|01_concepts]]
- [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/02_mistakes]]
- [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/03_assignments_notes]]
- [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/04-assignments]]
- [[020_Notes/tracks/Fullstack/99-Archive/Frontend/javascript/05_all_course_assignments]]