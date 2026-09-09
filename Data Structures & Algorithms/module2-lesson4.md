# Adding Data to an Array

Arrays are useful because programs often need to add new data to an existing collection.

For example, an online store may need to add a new product:

```text
Before:
[Laptop, Mouse, Keyboard]

        ↓ Add Monitor

After:
[Laptop, Mouse, Keyboard, Monitor]
```

JavaScript provides several ways to add data to an array.

In this lesson, we will focus on the most common method: **`push()`**.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Add a value to an array.
* Use the `push()` method.
* Understand where `push()` adds a value.
* Add multiple values to an array.
* Check the updated array.

---

## 1. Adding a Value with `push()`

The `push()` method adds a new value to the **end of an array**.

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products.push("Monitor");

console.log(products);
```

Output:

```text
["Laptop", "Mouse", "Keyboard", "Monitor"]
```

Visual:

```text
Before

┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘
    0        1          2


        push("Monitor")
               ↓


After

┌────────┬────────┬──────────┬─────────┐
│ Laptop │ Mouse  │ Keyboard │ Monitor │
└────────┴────────┴──────────┴─────────┘
    0        1          2          3
```

The new value is added at the end.

---

## 2. Adding Another Item

You can call `push()` whenever you need to add another value.

```js
const products = ["Laptop", "Mouse"];

products.push("Keyboard");
products.push("Monitor");

console.log(products);
```

Output:

```text
["Laptop", "Mouse", "Keyboard", "Monitor"]
```

The array grows as new values are added:

```text
["Laptop", "Mouse"]
        ↓
["Laptop", "Mouse", "Keyboard"]
        ↓
["Laptop", "Mouse", "Keyboard", "Monitor"]
```

---

## 3. Adding Multiple Values

`push()` can add more than one value at a time.

```js
const products = ["Laptop"];

products.push("Mouse", "Keyboard", "Monitor");

console.log(products);
```

Output:

```text
["Laptop", "Mouse", "Keyboard", "Monitor"]
```

Visual:

```text
Before

[Laptop]

       │
       │ push()
       ▼

[Laptop, Mouse, Keyboard, Monitor]
```

The values are added in the same order:

```text
Mouse → Keyboard → Monitor
```

---

## 4. Adding Numbers

Arrays are not limited to strings.

You can also add numbers.

```js
const scores = [85, 70, 92];

scores.push(78);

console.log(scores);
```

Output:

```text
[85, 70, 92, 78]
```

Visual:

```text
Before:

┌────┬────┬────┐
│ 85 │ 70 │ 92 │
└────┴────┴────┘

        ↓ push(78)

After:

┌────┬────┬────┬────┐
│ 85 │ 70 │ 92 │ 78 │
└────┴────┴────┴────┘
```

---

## 5. Adding Objects

Arrays can also store objects.

This is useful when working with real application data.

```js
const products = [
  { name: "Laptop", price: 1200 },
  { name: "Mouse", price: 25 }
];

products.push({
  name: "Keyboard",
  price: 50
});

console.log(products);
```

The collection now contains three products:

```text
products
   │
   ▼
┌──────────┬──────────┬────────────┐
│ Laptop   │ Mouse    │ Keyboard   │
│ $1200    │ $25      │ $50        │
└──────────┴──────────┴────────────┘
```

This pattern is common in applications that manage collections of users, products, orders, tasks, or other entities.

---

## 6. Checking the Updated Array

After adding data, you can check the array using `console.log()`.

```js
const tasks = ["Login", "Read Data"];

tasks.push("Save Data");

console.log(tasks);
```

Output:

```text
["Login", "Read Data", "Save Data"]
```

You can also check the number of items:

```js
console.log(tasks.length);
```

Output:

```text
3
```

Visual:

```text
tasks.length
     │
     ▼
┌──────┬──────────┬───────────┐
│ Login│ Read Data│ Save Data │
└──────┴──────────┴───────────┘
    0       1           2

Length = 3
```

Remember that **length** is the number of items, while the **last index** is `length - 1`.

---

## 7. What Does `push()` Return?

`push()` returns the **new length of the array**.

Example:

```js
const products = ["Laptop", "Mouse"];

const newLength = products.push("Keyboard");

console.log(newLength);
```

Output:

```text
3
```

The array now contains three items.

```text
["Laptop", "Mouse", "Keyboard"]
                         ↑
                    New length = 3
```

This can be useful when a program needs to know how many items are currently in the collection.

---

## 8. Adding Data from a Variable

The value passed to `push()` can come from a variable.

```js
const products = ["Laptop", "Mouse"];

const newProduct = "Keyboard";

products.push(newProduct);

console.log(products);
```

Output:

```text
["Laptop", "Mouse", "Keyboard"]
```

This is useful when new data comes from user input, an API, a form, or another part of the program.

---

## 9. Real-World Example

Imagine a simple task management application.

Initially:

```js
const tasks = [
  "Learn JavaScript",
  "Practice Arrays"
];
```

A user creates a new task:

```js
const newTask = "Build a Project";

tasks.push(newTask);

console.log(tasks);
```

Output:

```text
[
  "Learn JavaScript",
  "Practice Arrays",
  "Build a Project"
]
```

Visual:

```text
User creates a task
        │
        ▼
"Build a Project"
        │
        ▼
     push()
        │
        ▼
┌────────────────────┐
│ Learn JavaScript   │
│ Practice Arrays    │
│ Build a Project    │
└────────────────────┘
```

The array now contains the new task.

---

## 10. Important: `push()` Changes the Original Array

`push()` modifies the existing array.

Example:

```js
const products = ["Laptop", "Mouse"];

products.push("Keyboard");

console.log(products);
```

The original `products` array is changed:

```text
Before:
products → ["Laptop", "Mouse"]

After:
products → ["Laptop", "Mouse", "Keyboard"]
```

This is important to remember when working with arrays in larger programs.

---

## Key Idea

The **`push()`** method adds one or more values to the **end of an array**.

Basic syntax:

```js
array.push(value);
```

Example:

```js
const products = ["Laptop", "Mouse"];

products.push("Keyboard");

console.log(products);
```

Result:

```text
["Laptop", "Mouse", "Keyboard"]
```

Remember:

```text
push()
  │
  ▼
Adds data to the END of the array
```

**When a collection needs a new item at the end, `push()` is one of the simplest tools to use.**
