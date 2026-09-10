# Removing Data from an Array

Collections change over time.

A product may be discontinued, a task may be completed, or a user may be removed from a list.

JavaScript provides several ways to remove data from an array.

In this lesson, we will focus on **`pop()`** and **`splice()`**.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Remove the last value from an array.
* Use the `pop()` method.
* Remove a specific value using `splice()`.
* Understand how indexes are used when removing data.
* Check the updated array.

---

## 1. Removing the Last Value with `pop()`

The `pop()` method removes the **last value** from an array.

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products.pop();

console.log(products);
```

Output:

```text
["Laptop", "Mouse"]
```

Visual:

```text
Before

┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘
    0        1          2
                       ✕
                       │
                     pop()
                       │
                       ▼

After

┌────────┬────────┐
│ Laptop │ Mouse  │
└────────┴────────┘
    0        1
```

`pop()` always removes the item at the end.

---

## 2. What Does `pop()` Return?

`pop()` returns the value that was removed.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

const removedProduct = products.pop();

console.log(removedProduct);
```

Output:

```text
Keyboard
```

The array is also updated:

```js
console.log(products);
```

Output:

```text
["Laptop", "Mouse"]
```

Visual:

```text
products
   │
   ▼
[ Laptop, Mouse, Keyboard ]
                     │
                   pop()
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   Removed value            Updated array
    "Keyboard"              [Laptop, Mouse]
```

---

## 3. Removing a Specific Value

Sometimes we do not want to remove the last item.

For example:

```text
[Laptop, Mouse, Keyboard, Monitor]
```

We want to remove `"Mouse"`.

```text
[Laptop, Mouse, Keyboard, Monitor]
          ✕
          │
       Remove
```

For this situation, we can use **`splice()`**.

---

## 4. Using `splice()`

The `splice()` method can remove values from a specific position.

Basic syntax:

```js
array.splice(startIndex, deleteCount);
```

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard", "Monitor"];

products.splice(1, 1);

console.log(products);
```

Output:

```text
["Laptop", "Keyboard", "Monitor"]
```

Why?

```text
Index:      0        1          2          3
            │        │          │          │
            ▼        ▼          ▼          ▼
         ┌──────┬────────┬──────────┬─────────┐
Before:  │Laptop│  Mouse │ Keyboard │ Monitor │
         └──────┴────────┴──────────┴─────────┘
                     ✕
                     │
                splice(1, 1)
                     │
                     ▼
         ┌──────┬──────────┬─────────┐
After:   │Laptop│ Keyboard │ Monitor │
         └──────┴──────────┴─────────┘
```

The first argument, `1`, means:

> Start at index `1`.

The second argument, `1`, means:

> Remove `1` item.

---

## 5. Removing More Than One Value

`splice()` can remove multiple consecutive values.

Example:

```js
const products = [
  "Laptop",
  "Mouse",
  "Keyboard",
  "Monitor"
];

products.splice(1, 2);

console.log(products);
```

Output:

```text
["Laptop", "Monitor"]
```

The operation starts at index `1` and removes `2` items:

```text
Before:

Index:     0        1          2          3
           │        │          │          │
           ▼        ▼          ▼          ▼
        ┌──────┬────────┬──────────┬─────────┐
        │Laptop│  Mouse │ Keyboard │ Monitor │
        └──────┴────────┴──────────┴─────────┘
                  └────────────┘
                     Remove


After:

        ┌──────┬─────────┐
        │Laptop│ Monitor │
        └──────┴─────────┘
```

---

## 6. Removing One Item from the Middle

Consider this array:

```js
const tasks = [
  "Login",
  "Read Data",
  "Save Data",
  "Logout"
];
```

Suppose `"Save Data"` is no longer needed.

Its index is `2`.

```js
tasks.splice(2, 1);
```

The result is:

```text
["Login", "Read Data", "Logout"]
```

Visual:

```text
Before:

[Login] [Read Data] [Save Data] [Logout]
   0         1           2           3
                         ✕
                         │
                    splice(2, 1)
                         │
                         ▼
After:

[Login] [Read Data] [Logout]
   0         1           2
```

Notice that after removing an item, the indexes of later items can change.

---

## 7. `pop()` vs `splice()`

Both methods remove data, but they solve different problems.

| Method     | Purpose                             |
| ---------- | ----------------------------------- |
| `pop()`    | Removes the last item               |
| `splice()` | Removes items from a specific index |

Example:

```js
products.pop();
```

Means:

```text
Remove the LAST item
```

While:

```js
products.splice(1, 1);
```

Means:

```text
Start at index 1
Remove 1 item
```

Visual:

```text
             Removing Data
                   │
          ┌────────┴────────┐
          ▼                 ▼
       pop()             splice()
          │                 │
          ▼                 ▼
   Remove last item   Remove by index
```

---

## 8. Checking the Array Length

After removing data, the array becomes shorter.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.length);
```

Output:

```text
3
```

Remove one item:

```js
products.pop();

console.log(products.length);
```

Output:

```text
2
```

Visual:

```text
Before:

[Laptop] [Mouse] [Keyboard]
             Length = 3

              ↓ pop()

After:

[Laptop] [Mouse]
          Length = 2
```

---

## 9. Removing Data in a Real Program

Imagine a task management application.

A user completes a task:

```js
const tasks = [
  "Learn JavaScript",
  "Practice Arrays",
  "Build a Project"
];

tasks.splice(1, 1);

console.log(tasks);
```

Output:

```text
[
  "Learn JavaScript",
  "Build a Project"
]
```

The program removed `"Practice Arrays"`.

This pattern can be useful for managing:

* Tasks
* Products
* Orders
* Messages
* Users
* Notifications

---

## 10. Important: Removing Data Changes the Array

Like `push()`, these methods modify the original array.

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products.pop();

console.log(products);
```

The original array is now:

```text
["Laptop", "Mouse"]
```

It is not:

```text
["Laptop", "Mouse", "Keyboard"]
```

The array has been changed.

---

## 11. Choosing the Right Method

Use **`pop()`** when you need to remove the last item:

```js
products.pop();
```

Use **`splice()`** when you need to remove an item at a specific index:

```js
products.splice(2, 1);
```

A simple decision process:

```text
Need to remove data?
        │
        ▼
Is it the last item?
    │           │
   Yes          No
    │           │
    ▼           ▼
  pop()      splice()
```

---

## Key Idea

Arrays can change after they are created.

Use:

```js
array.pop();
```

to remove the **last item**.

Use:

```js
array.splice(startIndex, deleteCount);
```

to remove one or more items from a **specific position**.

Remember:

```text
pop()    → remove from the end
splice() → remove by position
```

**Understanding how to remove data is essential for managing collections that change over time.**
