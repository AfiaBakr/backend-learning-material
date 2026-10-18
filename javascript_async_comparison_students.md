# Callback Hell vs Promises vs Async/Await

**JavaScript Asynchronous Programming — Student Comparison Guide**

## 🎯 Learning Goal

Teeno examples mein same task perform hoga: pehle Data 1, phir Data 2, aur phir Data 3 receive karna.

Har data receive hone mein 1 second lagega. Difference sirf code likhne ke tareeqe ka hoga.

## 1. Callback Hell

Is example mein har next task, previous task ke callback ke andar likha gaya hai.

### Code

```javascript
function getData(id, callback) {
    setTimeout(() => {
        console.log("Data", id, "received");
        callback();
    }, 1000);
}

function getAllData() {
    console.log("Getting data 1...");

    getData(1, function () {
        console.log("Getting data 2...");

        getData(2, function () {
            console.log("Getting data 3...");

            getData(3, function () {
                console.log("All data received!");
            });
        });
    });
}

getAllData();
```

### Output

```text
Getting data 1...
Data 1 received
Getting data 2...
Data 2 received
Getting data 3...
Data 3 received
All data received!
```

### Explanation

Har next function ko previous function ke complete hone ke baad chalana hai, is liye callbacks nested hain.

Zyada steps hon to code pyramid jaisa ban jata hai, jise **Callback Hell** kehte hain.

## 2. Using Promises

Ab hum same task ko Promises aur `.then()` ke through perform karte hain.

### Code

```javascript
function getData(id) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Data", id, "received");
            resolve();
        }, 1000);
    });
}

function getAllData() {
    console.log("Getting data 1...");

    getData(1)
        .then(() => {
            console.log("Getting data 2...");
            return getData(2);
        })
        .then(() => {
            console.log("Getting data 3...");
            return getData(3);
        })
        .then(() => {
            console.log("All data received!");
        })
        .catch((error) => {
            console.log("Error:", error);
        });
}

getAllData();
```

### Output

```text
Getting data 1...
Data 1 received
Getting data 2...
Data 2 received
Getting data 3...
Data 3 received
All data received!
```

### Explanation

- `new Promise()` asynchronous operation ko represent karta hai.
- `resolve()` batata hai ke operation successfully complete ho gaya.
- `.then()` next step ko previous Promise complete hone par execute karta hai.
- `return getData(2)` important hai, kyun ke is se next `.then()` doosre task ke complete hone ka wait karta hai.
- `.catch()` errors handle karne ke liye use hota hai.

**Result:** Callback Hell ke muqable mein nesting kam ho gayi aur code zyada readable hai.

## 3. Using Async/Await

Ab same code ko `async` aur `await` ke saath likhte hain. Yeh approach sequential flow ko clearly show karti hai.

### Code

```javascript
function getData(id) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Data", id, "received");
            resolve();
        }, 1000);
    });
}

async function getAllData() {
    console.log("Getting data 1...");
    await getData(1);

    console.log("Getting data 2...");
    await getData(2);

    console.log("Getting data 3...");
    await getData(3);

    console.log("All data received!");
}

getAllData();
```

### Output

```text
Getting data 1...
Data 1 received
Getting data 2...
Data 2 received
Getting data 3...
Data 3 received
All data received!
```

### Explanation

- `async` function ko Promise-based asynchronous operations handle karne ke liye use hota hai.
- `await` Promise ke settle hone ka wait karta hai. Fulfilled Promise ki value milti hai.
- `await getData(1)` complete hone ke baad hi next statement execute hota hai.
- Code normal sequential code jaisa nazar aata hai, is liye samajhna aur maintain karna asaan hota hai.

## 4. Comparison Table

| Feature | Callback Hell | Promises | Async/Await |
|---|---|---|---|
| Main syntax | Nested callbacks | `.then()` | `async` / `await` |
| Readability | Mushkil ho sakti hai | Behtar | Usually sab se readable |
| Sequential tasks | Nested functions | Promise chaining | `await` one by one |
| Error handling | Callback mein manually | `.catch()` | `try...catch` |
| Beginner ke liye | Nesting samajhna zaroori | Chaining samajhna zaroori | Flow comparatively easy |

## 5. Class Mein Sab Se Important Concept

**Callback:** "Task complete ho, to yeh function chala dena."

**Promise:** "Yeh task future mein complete hoga; `.then()` mein next step likho."

**Async/Await:** "Promise ka result milne tak is async function mein wait karo, phir next line chalao."

## 6. Important Clarification

`async/await` Promises ko replace nahi karta. `await` normally Promise ke saath use hota hai.

Is liye teeno examples mein kaam same hai, lekin async/await ka code Promise-based hai aur use read karna zyada straightforward hai.

## 📌 Key Takeaways

- Callbacks functions ko baad mein execute karne ka tareeqa hain.
- Callback Hell mein multiple nested callbacks code ko difficult bana sakte hain.
- Promises asynchronous operations ko represent karte hain.
- `.then()` Promise fulfill hone ke baad next operation perform karne mein help karta hai.
- `.catch()` Promise chain mein errors handle karta hai.
- `async/await` Promise-based code ko readable banata hai.
- `await` current async function mein next statement ko Promise settle hone tak pause karta hai.

**Conclusion:** Teeno approaches sequential asynchronous tasks perform kar sakti hain. Modern JavaScript mein Promises aur async/await nested callbacks ke muqable mein code ko zyada readable aur maintainable bana sakte hain.