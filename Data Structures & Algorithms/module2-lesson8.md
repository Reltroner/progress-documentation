# Finding an Item in an Array

Programs often need to check whether a specific value exists inside an array.

For example:

* Is `"Laptop"` in the product list?
* Is `"Alice"` in the student list?
* Does the task list contain `"Practice Arrays"`?
* Is a specific score present?

An array can contain many values, so we need a way to **find an item**.

In JavaScript, one simple approach is to use the **`includes()`** method.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Check whether an item exists in an array.
* Use the `includes()` method.
* Understand the `true` and `false` results.
* Find the position of an item using `indexOf()`.
* Choose between `includes()` and `indexOf()` for basic array lookup.

---

## 1. Checking If an Item Exists

Suppose we have a product collection:

```js id="q7m2xp"
const products = ["Laptop", "Mouse", "Keyboard"];
```

We want to know whether `"Mouse"` exists.

Use `includes()`:

```js id="k4n8vz"
console.log(products.includes("Mouse"));
```

Output:

```text id="r5c1yd"
true
```

Visual:

```text id="a8p3wf"
products

┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘
             ▲
             │
       "Mouse" exists
             │
             ▼
           true
```

---

## 2. When the Item Does Not Exist

If the value is not in the array, `includes()` returns `false`.

```js id="v6k9qs"
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.includes("Monitor"));
```

Output:

```text id="x3m7ab"
false
```

Visual:

```text id="j9c4rw"
products

┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘

"Monitor"
    │
    ▼
Not found
    │
    ▼
  false
```

---

## 3. Understanding `true` and `false`

`includes()` returns a **Boolean** value.

A Boolean has two possible values:

```text id="n5q8yd"
true  → item exists
false → item does not exist
```

Example:

```js id="u2f6pk"
const products = ["Laptop", "Mouse", "Keyboard"];

const hasMouse = products.includes("Mouse");
const hasMonitor = products.includes("Monitor");

console.log(hasMouse);
console.log(hasMonitor);
```

Output:

```text id="w4r8cm"
true
false
```

---

## 4. Using the Result in an `if` Statement

The result of `includes()` can be used to make a decision.

```js id="p8d3vk"
const products = ["Laptop", "Mouse", "Keyboard"];

if (products.includes("Mouse")) {
  console.log("Product is available.");
}
```

Output:

```text id="t6x1qa"
Product is available.
```

Visual:

```text id="f3m8zp"
Check "Mouse"
      │
      ▼
products.includes("Mouse")
      │
      ▼
    true
      │
      ▼
Run the code inside if
```

If the item does not exist:

```js id="b7q2mn"
const products = ["Laptop", "Mouse", "Keyboard"];

if (products.includes("Monitor")) {
  console.log("Product is available.");
}
```

The message is not displayed because the condition is `false`.

---

## 5. Handling Both Results

You can use `else` when you want to handle both possibilities.

```js id="c9v4xr"
const products = ["Laptop", "Mouse", "Keyboard"];

if (products.includes("Monitor")) {
  console.log("Product is available.");
} else {
  console.log("Product is not available.");
}
```

Output:

```text id="h5m8yk"
Product is not available.
```

The decision process is:

```text id="z1r6qp"
          Check item
               │
               ▼
   products.includes("Monitor")
               │
        ┌──────┴──────┐
        ▼             ▼
      true           false
        │             │
        ▼             ▼
   Available      Not available
```

---

## 6. Finding the Position with `indexOf()`

Sometimes we do not only need to know whether an item exists.

We also need to know **where it is located**.

For this, JavaScript provides `indexOf()`.

Example:

```js id="m3x7qa"
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.indexOf("Mouse"));
```

Output:

```text id="n8v2cw"
1
```

The value `"Mouse"` is at index `1`.

```text id="s4k9pb"
Index:     0        1          2
           │        │          │
           ▼        ▼          ▼
        ┌──────┬────────┬──────────┐
        │Laptop│  Mouse │ Keyboard │
        └──────┴────────┴──────────┘
                     ▲
                     │
                indexOf()
                     │
                     ▼
                     1
```

---

## 7. When the Item Is Not Found with `indexOf()`

If `indexOf()` cannot find the value, it returns:

```text id="q2f7mx"
-1
```

Example:

```js id="v8c3kn"
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.indexOf("Monitor"));
```

Output:

```text id="d6p9wr"
-1
```

This means:

> The item was not found.

Visual:

```text id="x5m1qa"
Search for "Monitor"
        │
        ▼
      Array
        │
        ▼
   Not found
        │
        ▼
       -1
```

---

## 8. `includes()` vs `indexOf()`

Both methods can be used to find data, but they provide different results.

| Method       | Result           | Main Purpose                 |
| ------------ | ---------------- | ---------------------------- |
| `includes()` | `true` / `false` | Check whether an item exists |
| `indexOf()`  | Index or `-1`    | Find the position of an item |

Example:

```js id="k8r2vm"
const products = ["Laptop", "Mouse", "Keyboard"];

products.includes("Mouse");
// true

products.indexOf("Mouse");
// 1
```

Think of them like this:

```text id="c6w4pz"
             Need to find an item?
                     │
            ┌────────┴────────┐
            ▼                 ▼
     Need to know          Need its
      if it exists?         position?
            │                 │
            ▼                 ▼
       includes()         indexOf()
            │                 │
            ▼                 ▼
       true / false        index / -1
```

---

## 9. Using `indexOf()` to Update Data

Knowing the index can be useful when another array operation needs a position.

For example:

```js id="r7n3kc"
const products = ["Laptop", "Mouse", "Keyboard"];

const index = products.indexOf("Mouse");

if (index !== -1) {
  products[index] = "Wireless Mouse";
}

console.log(products);
```

Output:

```text id="p4x8ym"
["Laptop", "Wireless Mouse", "Keyboard"]
```

The process is:

```text id="w9q2vb"
Find "Mouse"
     │
     ▼
indexOf("Mouse")
     │
     ▼
     1
     │
     ▼
products[1]
     │
     ▼
Update value
```

This combines concepts from previous lessons:

```text
Find → Get index → Access index → Update value
```

---

## 10. Finding an Item in a Real Program

Imagine a task management application:

```js id="a5k8zn"
const tasks = [
  "Learn JavaScript",
  "Practice Arrays",
  "Build a Project"
];

const task = "Practice Arrays";

if (tasks.includes(task)) {
  console.log("Task exists.");
} else {
  console.log("Task not found.");
}
```

Output:

```text id="f2m7qx"
Task exists.
```

This is useful when an application needs to check whether something already exists before performing another action.

---

## 11. Finding Data Before Removing It

`indexOf()` can also help when a program needs to remove a specific value.

Example:

```js id="u6r9cp"
const tasks = [
  "Learn JavaScript",
  "Practice Arrays",
  "Build a Project"
];

const index = tasks.indexOf("Practice Arrays");

if (index !== -1) {
  tasks.splice(index, 1);
}

console.log(tasks);
```

Output:

```text id="e8v3mw"
[
  "Learn JavaScript",
  "Build a Project"
]
```

The process combines several array operations:

```text id="j3p7qa"
Find item
    │
    ▼
Get index
    │
    ▼
Remove item
    │
    ▼
Updated array
```

---

## 12. Case Sensitivity

String matching is case-sensitive.

For example:

```js id="n4c8vy"
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.includes("mouse"));
```

Output:

```text id="w7p2mz"
false
```

Why?

```text id="a9r5kx"
"Mouse"
   ≠
"mouse"
```

The uppercase `M` and lowercase `m` are different characters.

This is important when checking user input or other external data.

---

## 13. Finding Numbers

`includes()` can also check numbers.

```js id="x2v6qb"
const scores = [85, 70, 92, 78];

console.log(scores.includes(92));
```

Output:

```text id="m8k4zr"
true
```

And:

```js id="q5n9cw"
console.log(scores.includes(100));
```

Output:

```text id="y3p7va"
false
```

The same idea works for other basic values.

---

## 14. Finding Objects

When an array contains objects, finding an object works differently.

For example:

```js id="d7k2mp"
const products = [
  { id: 1, name: "Laptop" },
  { id: 2, name: "Mouse" }
];
```

This does **not** work as a general object lookup:

```js id="h4v8qx"
products.includes({ id: 1, name: "Laptop" });
```

The object created in the `includes()` call is a different object.

For arrays of objects, later array techniques such as `find()` are more appropriate.

For now, remember:

```text id="p6m1zy"
Simple values
   │
   ├── includes()
   └── indexOf()

Objects
   │
   └── Use object-specific search techniques
       such as find()
```

Object searching will be explored when working with more advanced array operations.

---

## Key Idea

JavaScript provides simple tools for finding data in an array.

Use:

```js id="b5x9kc"
array.includes(value);
```

when you only need to know whether the value exists.

Result:

```text
true / false
```

Use:

```js id="r8m3qp"
array.indexOf(value);
```

when you need the position of the value.

Result:

```text
index / -1
```

Remember:

```text id="v4k7ns"
includes() → "Does it exist?"
indexOf()  → "Where is it?"
```

**Finding data is a fundamental array operation that allows a program to make decisions based on the contents of a collection.**
