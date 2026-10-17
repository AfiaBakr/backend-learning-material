# ASYNC JAVASCRIPT
*Complete Lecture Notes* 

Callbacks • Promises • async/await • Fetch API • Error Handling   

Beginner-friendly notes with explanations, code examples, expected outputs, comparison tables, and classroom practice questions with solutions.  

## Part 1: Introduction to Asynchronous JavaScript

1. What is Synchronous JavaScript?   
In synchronous programming, instructions execute one after another, in order. The next instruction waits until the current instruction finishes.
```
console.log("First");
console.log("Second");
console.log("Third"); 
```
Output:
```
First
Second
Third
```
JavaScript executes these statements in order.

### 2. What is Asynchronous JavaScript?
Asynchronous JavaScript allows certain operations to start without blocking the rest of the program while they wait to finish. Examples include fetching data from an API, loading files, waiting for a timer, sending data to a server, and reading data from a database through a backend API.
```
console.log("First");
 
setTimeout(() => {
    console.log("Second");
}, 2000);
 
console.log("Third");
```
Output:
```
First
Third
Second
```
***Explanation:***
1.	"First" prints immediately.
2.	setTimeout() schedules its callback to run after approximately 2 seconds.
3.	JavaScript continues and prints "Third".
4.	When the timer has elapsed and the callback can run, "Second" prints.
The delay is a minimum wait, not a guarantee that the callback runs at the exact millisecond.
3. Why Do We Need Async JavaScript?
Imagine a website loading a user profile from a server. The server may take a few seconds to respond. Asynchronous techniques allow JavaScript to continue other work while the operation is pending, helping the application remain responsive.   

## Part 2: Callbacks
1. What is a Callback Function?
A callback is a function passed as an argument to another function so that it can be called later.
```
function greet(name, callback) {
    console.log("Hello, " + name);
    callback();
}
 
function sayWelcome() {
    console.log("Welcome to JavaScript!");
}
 
greet("Ali", sayWelcome);
```
Output:
```
Hello, Ali
Welcome to JavaScript!
```
***Explanation:***   
sayWelcome is passed as an argument to greet. Inside greet, `callback()` calls that function. Pass sayWelcome, not `sayWelcome()`, when you want to pass the function itself. 

### 2. Callback with setTimeout()
```
function showMessage() {
    console.log("Data loaded!");
}
 
setTimeout(showMessage, 2000);
console.log("Loading...");
```
Output:
```
Loading...
Data loaded!
```
The callback runs after the timer delay, so "Loading..." prints first.   
### 3. Real-Life Scenario: Order Processing
```
function prepareOrder(callback) {
    console.log("Preparing your order...");
    setTimeout(() => {
        console.log("Order is ready!");
        callback();
    }, 2000);
}
function notifyCustomer() {
    console.log("Please collect your order.");
}
prepareOrder(notifyCustomer);
```
Output:
```
Preparing your order...
Order is ready!
Please collect your order.
```
notifyCustomer is called after the order preparation callback runs.  

### 4. Callback Hell
When many asynchronous callbacks are nested inside one another, the code becomes difficult to read and maintain.    This is commonly called callback hell.
```
setTimeout(() => {
    console.log("Step 1");
    setTimeout(() => {
        console.log("Step 2");
        setTimeout(() => {
            console.log("Step 3");
        }, 1000);
    }, 1000);
}, 1000);
```
*Promises* and *async/await* provide cleaner ways to handle many such workflows.

## Part 3: Promises
### 1. What is a Promise?
A Promise is a JavaScript object that represents the eventual result of an asynchronous operation. The result may be a successful value or an error, such as when requesting student records from a server.
### 2. Three States of a Promise
•	Pending: the operation has not finished yet.   
•	Fulfilled: the operation succeeded.    
•	Rejected: the operation failed.    
A settled Promise is either fulfilled or rejected.
### 3. Creating a Promise
The Promise constructor receives a function with two ***parameters: *** `resolve and reject`. `resolve()` fulfills the Promise; `reject()` rejects it.     
```
const myPromise = new Promise((resolve, reject) => {
    let success = true;
    if (success) {
        resolve("Operation successful!");
    } else {
        reject("Operation failed!");
    }
});
console.log(myPromise);
```
The Promise settles immediately in this example, although developer tools may display its state according to their own presentation.

### 4. Using `.then()` and `.catch()`

`.then()` handles fulfillment. `.catch()` handles a rejection in the Promise chain.
```
const myPromise = new Promise((resolve, reject) => {
    let success = true;
    if (success) {
        resolve("Data loaded successfully!");
    } else {
        reject("Unable to load data!");
    }
});
myPromise
    .then(result => console.log(result))
    .catch(error => console.log(error));
```
Output when success is true:
```
Data loaded successfully!
If success is false, the output is:
Unable to load data!
```
### 5. Promise with a Timer
```
function getData() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Student data received!"), 2000);
    });
}
getData().then(data => console.log(data));
console.log("Request started...");
```
Output:
```
Request started...
Student data received!
```
The Promise resolves after approximately 2 seconds.

### 6. Promise Chaining
Promises allow multiple operations to be performed in sequence. Returning a value from `.then()` makes it available to the next `.then()`. Returning a Promise makes the chain wait for it to settle.
```
Promise.resolve(5)
    .then(number => number * 2)
    .then(result => result + 10)
    .then(finalResult => console.log(finalResult));
```
Output:
```
20
```
The initial `value is 5;` the first `.then()` `returns 10;` the second `returns 20; `the final `.then()` `prints 20.`

### 7. Promise.all()

`Promise.all()` runs multiple Promise-based operations concurrently and fulfills when all fulfill. If any input Promise rejects, the combined Promise rejects.
```
const p1 = Promise.resolve("Students loaded");
const p2 = Promise.resolve("Courses loaded");
const p3 = Promise.resolve("Marks loaded");
 
Promise.all([p1, p2, p3])
    .then(results => console.log(results))
    .catch(error => console.log("Error:", error));
```
Output:
```
["Students loaded", "Courses loaded", "Marks loaded"]
```
This is useful when multiple independent requests need to succeed before continuing.

## Part 4: Async/Await
### 1. What is async/await?
`async/await` is syntax that makes Promise-based asynchronous code easier to read. async makes a function return a Promise.
Await pauses that async function until a Promise settles, then gives the fulfilled value or throws the rejection reason. await does not block the entire JavaScript program; it pauses the current async function.

### 2. Using async
```
async function greet() {
    return "Hello Students!";
}
greet().then(message => console.log(message));
Output:
Hello Students!
Although the function returns a normal string, calling greet() returns a Promise fulfilled with that string.
```
### 3. Using await
```
function getData() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Data received!"), 2000);
    });
}
async function showData() {
    console.log("Loading...");
    const result = await getData();
    console.log(result);
}
showData();
```
Output:
```
Loading...
Data received!
```
The await expression waits for getData() to fulfill before assigning its result to result.

### 4. Promise vs Async/Await

Promise syntax:
```
function getUser() {
    return Promise.resolve({ name: "Ali" });
}
getUser()
    .then(user => console.log(user.name))
    .catch(error => console.log(error));
```
Async/await syntax:
```
async function showUser() {
    try {
        const user = await getUser();
        console.log(user.name);
    } catch (error) {
        console.log(error);
    }
}
showUser();
```
Both handle the same Promise-based operation. async/await often makes sequential logic easier to follow.

### 5. Sequential vs Concurrent Awaiting
If one operation depends on the previous one, sequential await is appropriate.
```
const user = await getUser();
const orders = await getOrders(user.id);
```
If two operations are independent, they can be started together:
```
const [users, courses] = await Promise.all([
    getUsers(),
    getCourses()
]);
```
The second example allows both Promise-based operations to run concurrently instead of waiting for one before starting the other.
## Part 5: Fetch API
### 1. What is the Fetch API?
The Fetch API is a built-in browser API used to make `HTTP `requests to servers and APIs. It can retrieve data using GET, send data using `POST`, update data using `PUT `or `PATCH`, and delete data using DELETE.
`fetch()` returns a Promise that fulfills with a Response object when a response is received. An `HTTP error` status such as `404` does not automatically reject the Fetch Promise, so check response.ok.
### 2. Basic GET Request
This example uses JSONPlaceholder, a public testing API.
```
fetch("https://jsonplaceholder.typicode.com/users/1")
    .then(response => response.json())
    .then(user => console.log(user))
    .catch(error => console.log("Request failed:", error));
```
The response body is parsed as JSON, and the resulting JavaScript object is printed. Example response data includes:
```
{
    id: 1,
    name: "Leanne Graham",
    username: "Bret"
}
```
The API returns additional fields as well.
### 3. Understanding the Fetch Steps
```
fetch("https://jsonplaceholder.typicode.com/users/1")
```
Sends the request and returns a Promise.
```
.then(response => response.json())
```
Reads the response body and parses its JSON content. This also returns a Promise.
```
.then(user => console.log(user))
```
Receives the parsed JavaScript object.
```
.catch(error => console.log(error))
```
Handles errors such as network failures or errors thrown earlier in the chain.
***Important:*** this basic example does not explicitly check whether the HTTP status was successful. The next example adds that check.
### 4. GET Request with async/await
```
async function getUser() {
    try {
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/users/1"
        );
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        const user = await response.json();
        console.log(user);
    } catch (error) {
        console.log("Error:", error.message);
    }
}
getUser();
```
This is a safer pattern because it checks the HTTP response status before using the response body.
### 5. POST Request — Sending Data
A POST request can send data to a server. JSON Placeholder simulates creating a post; it does not permanently save it.
```
async function createPost() {
    try {
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/posts",
            {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    title: "JavaScript",
                    body: "Learning Fetch API",
                    userId: 1
                })
            }
        );
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        const data = await response.json();
        console.log("Created post:", data);
    } catch (error) {
        console.log("Error:", error.message);
    }
}
createPost();
```
•	method specifies the HTTP method.
•	headers tells the server the request body is JSON.
•	`JSON.stringify()` converts a JavaScript object into a JSON string.
•	`response.json()` parses the JSON response into a ***JavaScript value.***
## 6. Fetch Request Flow
     5.	Call fetch(url).
     6.	Receive the Response object.
     7.	Check response.ok.
     8.	Parse the body using response.json().
     9.	Use the data or handle an error.

## Part 6: Error Handling in JavaScript
### 1. What is Error Handling?
Error handling allows us to detect and respond to problems without leaving the application in an unexpected state.   
•	Invalid user input.  
•	A network connection failure.  
•	A server returning an error status.  
•	Accessing a missing property incorrectly.  
•	Invalid JSON data.  
### 2. try...catch
try...catch handles errors thrown while executing code.
```
try {
    let result = 10 / 0;
    console.log(result);
    console.log(userName);
} catch (error) {
    console.log("Something went wrong!");
}
```
Output:
```
Infinity
Something went wrong!
```
JavaScript allows division by zero for numbers, producing Infinity. The undefined variable userName causes a ReferenceError, which is caught by catch.
### 3. Using throw
The throw statement lets us create an error when a condition is invalid.
```
function checkAge(age) {
    if (age < 18) {
        throw new Error("You must be at least 18.");
    }
    return "Access allowed";
}
try {
    console.log(checkAge(16));
} catch (error) {
    console.log(error.message);
}
```
Output:
```
You must be at least 18.
```
throw new Error(...) stops the current flow unless the error is caught by an appropriate handler.
### 4. Error Handling with Promises
Use .catch() to handle a rejected Promise or an error thrown earlier in the Promise chain.
```
Promise.reject(new Error("Unable to load data"))
    .then(result => console.log(result))
    .catch(error => console.log("Error:", error.message));
```
Output:
```
Error: Unable to load data
```
### 5. Error Handling with async/await
```
async function loadData() {
    try {
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/invalid-endpoint"
        );
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.log("Failed to load data:", error.message);
    }
}
loadData();
```
The example checks response.ok, so an HTTP error status is turned into an exception that the catch block can handle.
### 6. Three Important Fetch Error Cases
| Error type | Does `fetch()` reject automatically? | How to handle it |
|---|---|---|
| Network failure | Usually yes | `.catch()` or `try...catch` |
| HTTP 404 or 500 | No | Check `response.ok` |
| Invalid JSON response | `response.json()` Promise rejects | `.catch()` or `try...catch` |

This distinction is important when working with real APIs.
## Part 7: Quick Comparison
|Concept	|Main purpose	|Common syntax|
|---|---|---|
|Callback	|Pass a function to be called later	|setTimeout(() => {}, 1000)|
|Promise	|Represent a future result	|.then() / .catch()|
|Async/await	|Write Promise-based code readably	|await somePromise()|
|Fetch API	|Make HTTP requests	|fetch(url)|
|Error handling	|Detect and handle failures	|try...catch, .catch(), throw|

***Key takeaway: ***
 Fetch returns a Promise, async/await lets us work with that Promise, and error handling helps us respond when the operation fails. Callbacks are another way to run a function after an event or operation.
### Part 8: Practice Questions with Solutions
### Q1. Predict the output.
```
Question code:
console.log("A");
setTimeout(() => console.log("B"), 1000);
console.log("C");
```
Solution:
```
A
C
B
```
### Q2. Create a callback function that prints "Order delivered!" after "Order prepared!".
Solution:
```
function prepareOrder(callback) {
    console.log("Order prepared!");
    callback();
}
function delivered() {
    console.log("Order delivered!");
}
prepareOrder(delivered);
```
### Q3. Create a Promise that resolves with the message "Success!".
Solution:
```
const task = new Promise(resolve => {
    resolve("Success!");
});
task.then(message => console.log(message));
```
### Q4. What is the output?
```
Question code:
Promise.resolve(10)
    .then(n => n * 2)
    .then(n => console.log(n));
```
Solution:
```
20
```
### Q5. Write an async function that awaits a Promise resolving to "Hello".
Solution:
```
async function showMessage() {
    const message = await Promise.resolve("Hello");
    console.log(message);
}
showMessage();
```
### Q6. Fetch user 1 and print their name. Include HTTP error handling.
Solution:
```
async function getUser() {
    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
        if (!response.ok) throw new Error(`HTTP error: ${response.status}`);
        const user = await response.json();
        console.log(user.name);
    } catch (error) {
        console.log(error.message);
    }
}
getUser();
```
### Q7. What is wrong with this Fetch code?
Question code:
```
fetch("/api/users")
    .then(response => response.json())
    .then(users => console.log(users));
```
Solution:
```
It has no error handling, and it does not check response.ok. A 404 or 500 response does not automatically reject fetch(). Add an HTTP status check and a catch handler.
```
### Q8. Handle an age below 18 using throw and try...catch.
Solution:
```
function checkAge(age) {
    if (age < 18) throw new Error("Age must be 18 or above");
    return "Allowed";
}
try {
    console.log(checkAge(16));
} catch (error) {
    console.log(error.message);
}
```
***Recommended Teaching Sequence***   

    10. Synchronous vs asynchronous JavaScript.   
    11.	Callbacks and callback hell.   
    12.	Promises, .then(), .catch(), and Promise.all().   
    13.	async/await.   
    14.	Fetch API with GET and POST requests.   
    15. Error handling using try...catch, throw, and HTTP status checks.   
This sequence helps students understand the purpose of each feature before combining them into a real API request.
