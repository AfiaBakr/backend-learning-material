# Async JavaScript — Complete Lecture Notes

Beginner-friendly lecture notes covering Callbacks, Promises, async/await, Fetch API, and Error Handling in JavaScript.

## 📚 Topics Covered

### Part 1: Introduction to Asynchronous JavaScript
- Synchronous vs. asynchronous JavaScript
- How `setTimeout()` works
- Why asynchronous programming is important
- Execution order and delays

### Part 2: Callback Functions
- What is a callback function?
- Passing functions as arguments
- Callbacks with `setTimeout()`
- Real-life example: Order processing
- Callback Hell
- Practice questions with solutions

### Part 3: Promises
- What is a Promise?
- Three states of a Promise:
  - Pending
  - Fulfilled
  - Rejected
- Creating Promises using `new Promise()`
- Handling results with `.then()`
- Handling errors with `.catch()`
- Promises with timers
- Promise chaining
- Sequential asynchronous operations

### Part 4: Async/Await
- Understanding `async` and `await`
- Using async functions
- Waiting for Promises with `await`
- Promise syntax vs. async/await
- Sequential vs. concurrent operations
- Using `Promise.all()`

### Part 5: Fetch API
- Introduction to the Fetch API
- Making GET requests
- Fetching data from public APIs
- Understanding the Fetch request flow
- Using Fetch with async/await
- Sending data using POST requests
- Working with JSON data
- Checking HTTP response status using `response.ok`

### Part 6: Error Handling in JavaScript
- What is error handling?
- Using `try...catch`
- Creating errors with `throw`
- Handling rejected Promises
- Error handling with async/await
- Network errors vs. HTTP errors
- Handling invalid JSON responses

### Part 7: Quick Comparison
A comparison of:
- Callbacks
- Promises
- Async/await
- Fetch API
- Error handling

### Part 8: Practice Questions with Solutions
- Predicting asynchronous output
- Creating callback functions
- Creating and handling Promises
- Understanding Promise chaining
- Writing async/await functions
- Fetching API data with HTTP error handling
- Identifying errors in Fetch code
- Using `throw` and `try...catch`

## 🎯 Learning Objectives

After studying these notes, students should be able to:

- Understand synchronous and asynchronous JavaScript.
- Create and use callback functions.
- Explain and implement Promises.
- Handle successful and failed asynchronous operations.
- Use `.then()` and `.catch()` correctly.
- Write asynchronous code using `async/await`.
- Fetch data from APIs using GET and POST requests.
- Parse JSON responses.
- Handle network errors and HTTP error statuses.
- Apply asynchronous JavaScript concepts to practical problems.

## 🛠️ Technologies Used

- JavaScript (ES6+)
- Promises
- Async/Await
- Fetch API
- JSON
- JSONPlaceholder testing API
- Browser Developer Tools

## 🌐 Example API

The notes use [JSONPlaceholder](https://jsonplaceholder.typicode.com/) as a public testing API for practicing GET and POST requests.

Example endpoint:

`https://jsonplaceholder.typicode.com/users/1`

## 📖 Recommended Learning Sequence

1. Synchronous vs. asynchronous JavaScript
2. Callback functions and Callback Hell
3. Promises, `.then()`, and `.catch()`
4. Async/await and `Promise.all()`
5. Fetch API with GET and POST requests
6. Error handling with `try...catch`, `throw`, and HTTP status checks
7. Practice questions and coding exercises

## 👩‍💻 Practice and Revision

These lecture notes include explanations, code examples, expected outputs, comparison tables, classroom exercises, and solutions to help beginners understand asynchronous JavaScript step by step.

**Key Takeaway:** Callbacks, Promises, async/await, and the Fetch API help JavaScript work with asynchronous operations. Proper error handling makes these operations more reliable.

---

**Subject:** JavaScript  
**Topic:** Asynchronous JavaScript  
**Level:** Beginner  
**Purpose:** Lecture notes, practice, and revision