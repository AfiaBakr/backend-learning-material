# JAVASCRIPT DESTRUCTURING

*Lecture Notes • Beginner Level • Theory + Examples*

## 1. What is Destructuring?

Destructuring is an ES6 feature in JavaScript that lets us extract values from arrays or properties from objects and store them in variables easily. Instead of accessing each value separately, we can extract multiple values in one statement.

### Without destructuring

```javascript
let student = ["Ali", 21, "Software Engineering"];

let name = student[0];
let age = student[1];
let department = student[2];

console.log(name);
console.log(age);
console.log(department);
```

### With destructuring

```javascript
let student = ["Ali", 21, "Software Engineering"];

let [name, age, department] = student;

console.log(name);
console.log(age);
console.log(department);
```

**Output:**
```text
Ali
21
Software Engineering
```

There are two main types: array destructuring and object destructuring.

---

## 2. Array Destructuring

Array destructuring extracts values according to their position or index.

### Example 1: Basic array destructuring

```javascript
let colors = ["Red", "Green", "Blue"];

let [first, second, third] = colors;

console.log(first);
console.log(second);
console.log(third);
```

**Output:**
```text
Red
Green
Blue
```

### Example 2: Skipping values

Leave an empty space between commas to skip an array element.

```javascript
let numbers = [10, 20, 30, 40, 50];

let [first, , third, , fifth] = numbers;

console.log(first);
console.log(third);
console.log(fifth);
```

**Output:**
```text
10
30
50
```

### Example 3: Default values

A default value is used when the extracted value is `undefined`.

```javascript
let student = ["Laiba", 21];

let [name, age, city = "Karachi"] = student;

console.log(name);
console.log(age);
console.log(city);
```

**Output:**
```text
Laiba
21
Karachi
```

Another example:

```javascript
let [a = 100] = [];
console.log(a); // 100

let [b = 100] = [0];
console.log(b); // 0
```

**Note:** A default value is used only when the value is `undefined`, not when it is `0`, `false`, or `null`.

### Example 4: Swapping variables

```javascript
let a = 10;
let b = 20;

[a, b] = [b, a];

console.log(a);
console.log(b);
```

**Output:**
```text
20
10
```

Destructuring lets us swap two variable values in one statement without a temporary variable.

---

## 3. Object Destructuring

Object destructuring extracts values using property names, not positions. Property order does not determine which value is assigned.

### Example 1: Basic object destructuring

```javascript
let student = {
    name: "Ali",
    age: 21,
    city: "Karachi"
};

let { name, age, city } = student;

console.log(name);
console.log(age);
console.log(city);
```

**Output:**
```text
Ali
21
Karachi
```

### Example 2: Extract selected properties

```javascript
let employee = {
    name: "Ahmed",
    age: 25,
    department: "IT",
    salary: 80000
};

let { name, salary } = employee;

console.log(name);
console.log(salary);
```

**Output:**
```text
Ahmed
80000
```

You do not need to extract every property. Here, `age` and `department` are not extracted.

### Example 3: Renaming variables

```javascript
let student = {
    name: "Sara",
    age: 22
};

let { name: studentName, age: studentAge } = student;

console.log(studentName);
console.log(studentAge);
```

**Output:**
```text
Sara
22
```

**Syntax:**

```javascript
let { propertyName: newVariableName } = object;
```

This creates new variable names; it does not rename the original object properties.

### Example 4: Default values in objects

```javascript
let student = {
    name: "Hassan",
    age: 20
};

let { name, age, city = "Karachi" } = student;

console.log(name);
console.log(age);
console.log(city);
```

**Output:**
```text
Hassan
20
Karachi
```

### Example 5: Nested object destructuring

```javascript
let student = {
    name: "Ali",
    address: {
        city: "Karachi",
        country: "Pakistan"
    }
};

let {
    address: { city, country }
} = student;

console.log(city);
console.log(country);
```

**Output:**
```text
Karachi
Pakistan
```

Here, `city` and `country` are extracted from the nested `address` object.

---

## 4. Destructuring in Functions

Destructuring is useful when a function receives an object as an argument.

### Without destructuring

```javascript
function displayStudent(student) {
    console.log(student.name);
    console.log(student.age);
}

displayStudent({
    name: "Laiba",
    age: 21
});
```

### With destructuring

```javascript
function displayStudent({ name, age }) {
    console.log(name);
    console.log(age);
}

displayStudent({
    name: "Laiba",
    age: 21
});
```

**Output:**
```text
Laiba
21
```

This pattern is commonly used with API responses, configuration objects, and React component props.

---

## 5. Rest Syntax with Destructuring

The rest syntax (`...`) collects the remaining elements or properties into a new array or object.

### Array example

```javascript
let numbers = [10, 20, 30, 40, 50];

let [first, second, ...remaining] = numbers;

console.log(first);
console.log(second);
console.log(remaining);
```

**Output:**
```text
10
20
[30, 40, 50]
```

### Object example

```javascript
let employee = {
    name: "Ahmed",
    age: 25,
    department: "IT",
    salary: 80000
};

let { name, ...otherDetails } = employee;

console.log(name);
console.log(otherDetails);
```

**Output:**
```text
Ahmed
{ age: 25, department: 'IT', salary: 80000 }
```

The rest variable must be the last item in its destructuring pattern.

---

## 6. Quick Comparison

| Feature | Array Destructuring | Object Destructuring |
|---|---|---|
| Syntax | `[]` | `{}` |
| Extracts by | Position / index | Property name |
| Example | `let [a, b] = arr;` | `let { name, age } = obj;` |
| Skipping | Use empty commas | Omit properties |
| Defaults | Supported | Supported |
| Renaming | Choose variable names | `property: newVariable` |

---

## 7. Practice Questions

Predict the output before running each code snippet.

### Question 1

```javascript
let arr = [5, 10, 15];
let [a, b] = arr;
console.log(b);
```

**Answer:** `10` — `b` receives the second array element.

### Question 2

```javascript
let [a = 100] = [50];
console.log(a);
```

**Answer:** `50` — the default is used only when the value is `undefined`.

### Question 3

```javascript
let user = { name: "Ali", age: 20 };
let { age } = user;
console.log(age);
```

**Answer:** `20` — object destructuring extracts the `age` property.

### Question 4

```javascript
let [first, ...rest] = [1, 2, 3, 4];
console.log(rest);
```

**Answer:** `[2, 3, 4]` — rest collects the remaining elements into an array.

### Question 5

```javascript
let student = { name: "Sara" };
let { name: studentName } = student;
console.log(studentName);
```

**Answer:** `Sara` — `name` is assigned to the variable `studentName`.

---

## 8. Suggested Teaching Sequence

1. Explain the problem of repeatedly accessing array indexes and object properties.
2. Teach basic array destructuring and skipping elements.
3. Teach object destructuring and property renaming.
4. Explain default values and swapping variables.
5. Finish with nested destructuring, rest syntax, and function parameters.

---

## Final Takeaway

Destructuring does not change the original array or object. It provides a convenient way to extract values into variables. Arrays are destructured by position, while objects are destructured by property name.
