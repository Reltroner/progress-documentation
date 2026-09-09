# Accessing Data by Index

An array stores values in a specific order.

To access a value inside an array, JavaScript uses an **index**.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Understand what an array index is.
* Access values using an index.
* Understand why array indexes start at `0`.
* Access the first, last, and other values in an array.
* Use indexes in JavaScript programs.

---

## 1. What Is an Index?

An **index** is the position of a value inside an array.

JavaScript arrays start counting from **0**.

For example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];
```

The array looks like this:

```text
Index:     0          1           2
           │          │           │
           ▼          ▼           ▼
        ┌──────┬──────────┬──────────┐
        │Laptop│  Mouse   │ Keyboard │
        └──────┴──────────┴──────────┘
```

So:

* `"Laptop"` → index `0`
* `"Mouse"` → index `1`
* `"Keyboard"` → index `2`

---

## 2. Accessing an Array Value

Use square brackets with the index:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products[0]);
```

Output:

```text
Laptop
```

You can access other values:

```js
console.log(products[1]);
console.log(products[2]);
```

Output:

```text
Mouse
Keyboard
```

---

## 3. Why Does JavaScript Start at 0?

The first position in an array is index `0`.

Think of it like counting positions:

```text
First value   → 0
Second value  → 1
Third value   → 2
Fourth value  → 3
```

For an array:

```js
const scores = [85, 70, 92, 78];
```

The indexes are:

```text
Index
  0      1      2      3
  │      │      │      │
  ▼      ▼      ▼      ▼
┌────┬────┬────┬────┐
│ 85 │ 70 │ 92 │ 78 │
└────┴────┴────┴────┘
```

Therefore:

```js
scores[0]; // 85
scores[1]; // 70
scores[2]; // 92
scores[3]; // 78
```

---

## 4. Accessing the First Value

The first value is always at index `0`.

```js
const students = ["Alice", "Bob", "Charlie"];

console.log(students[0]);
```

Output:

```text
Alice
```

---

## 5. Accessing the Last Value

You can access the last value using its index.

For example:

```js
const students = ["Alice", "Bob", "Charlie"];

console.log(students[2]);
```

Output:

```text
Charlie
```

However, hard-coding the index is not always useful.

JavaScript provides `.length` to determine how many values are in an array.

```js
const students = ["Alice", "Bob", "Charlie"];

console.log(students.length);
```

Output:

```text
3
```

The last index is:

```text
length - 1
```

So:

```js
console.log(students[students.length - 1]);
```

Output:

```text
Charlie
```

Visual:

```text
Length = 3

Index:     0        1         2
           │        │         │
           ▼        ▼         ▼
        ┌──────┬────────┬─────────┐
        │Alice │  Bob   │ Charlie │
        └──────┴────────┴─────────┘
                              ▲
                              │
                    Last index = 3 - 1
                              │
                              ▼
                              2
```

---

## 6. Using an Index with a Variable

An index can also be stored in a variable.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

const index = 1;

console.log(products[index]);
```

Output:

```text
Mouse
```

This is useful when the index comes from another part of a program.

---

## 7. What Happens If the Index Does Not Exist?

If you try to access an index that does not exist, JavaScript returns:

```text
undefined
```

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products[5]);
```

Output:

```text
undefined
```

The array only has indexes:

```text
0
1
2
```

Index `5` does not exist.

---

## 8. Accessing Data Inside a Real Program

Imagine an application storing product names:

```js
const products = [
  "Laptop",
  "Mouse",
  "Keyboard",
  "Monitor"
];

const selectedProduct = products[2];

console.log(selectedProduct);
```

Output:

```text
Keyboard
```

The program selects the value at index `2`.

```text
products
    │
    ▼
┌────────┬────────┬──────────┬─────────┐
│ Laptop │ Mouse  │ Keyboard │ Monitor │
└────────┴────────┴──────────┴─────────┘
    0        1          2          3
                       ▲
                       │
                  selected
                       │
                       ▼
                   Keyboard
```

This pattern is common when a program needs to work with a specific item in a collection.

---

## 9. Accessing Multiple Values

You can access different values from the same array:

```js
const scores = [85, 70, 92, 78];

const firstScore = scores[0];
const secondScore = scores[1];
const highestScore = scores[2];

console.log(firstScore);
console.log(secondScore);
console.log(highestScore);
```

Output:

```text
85
70
92
```

Each variable accesses a different position in the array.

---

## Key Idea

**An array index identifies the position of a value inside an array.**

Remember:

```text
First value  → index 0
Second value → index 1
Third value  → index 2
```

To access a value:

```js
array[index]
```

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products[1]);
```

Output:

```text
Mouse
```

**Arrays use indexes to let programs access specific values quickly and directly.**
