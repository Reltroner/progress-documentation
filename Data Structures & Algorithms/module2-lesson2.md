# What Is an Array?

An **array** is a JavaScript data structure used to store **multiple values in an ordered collection**.

```text id="a7k3m2"
Array
  │
  ▼
┌────┬────┬────┬────┐
│ 85 │ 70 │ 92 │ 78 │
└────┴────┴────┴────┘
```

Instead of storing each value in a separate variable, we can store them together in one array.

```js id="q4m8vz"
const scores = [85, 70, 92, 78];
```

---

## Lesson Objectives

By the end of this lesson, you should be able to:

* **Define** what an array is.
* **Create** an array in JavaScript.
* **Identify** the values stored in an array.
* **Understand** that array values have an order.
* **Recognize** arrays as a common way to store collections.

---

## 1. An Array Stores Multiple Values

Without an array:

```js id="v2n6px"
const score1 = 85;
const score2 = 70;
const score3 = 92;
const score4 = 78;
```

Visualized:

```text id="r8c4wy"
score1 → 85

score2 → 70

score3 → 92

score4 → 78
```

With an array:

```js id="k5t9qa"
const scores = [85, 70, 92, 78];
```

Visualized:

```text id="m3p7xz"
scores
   │
   ▼
┌────┬────┬────┬────┐
│ 85 │ 70 │ 92 │ 78 │
└────┴────┴────┴────┘
```

One variable can now refer to the entire collection.

---

## 2. Creating an Array

An array uses square brackets:

```js id="n6w2kj"
const scores = [85, 70, 92, 78];
```

Basic structure:

```text id="t4v8yc"
const scores = [85, 70, 92, 78];
             └────────────────┘
                    Array
```

The values are separated by commas.

```text id="j9q3mp"
[ 85 , 70 , 92 , 78 ]
  ▲    ▲    ▲    ▲
  │    │    │    │
Value Value Value Value
```

---

## 3. Arrays Keep Values in Order

Array values have a specific order.

```js id="p7x4bz"
const products = [
  "Laptop",
  "Mouse",
  "Keyboard",
  "Monitor"
];
```

Visualized:

```text id="w3k8qn"
┌──────────┬────────┬──────────┬─────────┐
│  Laptop  │ Mouse  │ Keyboard │ Monitor │
└──────────┴────────┴──────────┴─────────┘
     1         2          3         4
```

The order matters because each value has a position.

JavaScript uses an **index** to identify that position.

```text id="c6m2vr"
Value:
 Laptop    Mouse    Keyboard    Monitor
   │         │          │          │
   ▼         ▼          ▼          ▼
Index:
   0         1          2          3
```

Array indexes start at **0**, not 1.

We will explore indexes in the next lesson.

---

## 4. Arrays Can Store Different Types of Values

JavaScript arrays are **not required to contain only one data type**.

For example:

```js id="z8f5kt"
const values = [10, "Hello", true];
```

Visualized:

```text id="y4n7qx"
┌────┬─────────┬──────┐
│ 10 │ "Hello" │ true │
└────┴─────────┴──────┘
  ↑       ↑        ↑
Number   Text   Boolean
```

However, arrays are often used to store values that belong to the same kind of collection:

```js id="b2r6mw"
const scores = [85, 70, 92, 78];
```

```text id="k9v3ps"
Scores
  │
  ├── 85
  ├── 70
  ├── 92
  └── 78
```

This makes the data easier to understand and process.

---

## 5. Arrays Can Store Objects

Arrays can also contain objects.

For example:

```js id="f5q8cn"
const users = [
  { name: "Alex", age: 25 },
  { name: "Sarah", age: 28 },
  { name: "John", age: 31 }
];
```

Visualized:

```text id="u3m7za"
users
  │
  ├── User
  │    ├── name: Alex
  │    └── age: 25
  │
  ├── User
  │    ├── name: Sarah
  │    └── age: 28
  │
  └── User
       ├── name: John
       └── age: 31
```

This is common in real applications.

For example:

```text id="x6r2jp"
Application
     │
     ▼
Collection of Users
     │
     ▼
Array of Objects
```

---

## 6. Arrays Are Useful for Collections

Arrays are useful when a program needs to manage an ordered group of values.

Common examples:

```text id="q5w9kc"
Array
  │
  ├── Products
  ├── Students
  ├── Scores
  ├── Tasks
  ├── Messages
  └── Orders
```

For example:

```js id="m8z4tr"
const tasks = [
  "Read email",
  "Fix bug",
  "Deploy application"
];
```

Visualized:

```text id="h7p3vx"
tasks
  │
  ▼
┌──────────────┬─────────┬────────────────────┐
│ Read email   │ Fix bug │ Deploy application │
└──────────────┴─────────┴────────────────────┘
```

---

## 7. An Array Is One Collection

The important idea is that the array represents the **whole collection**.

```text id="r4k8yb"
                 scores
                   │
                   ▼
        ┌─────────────────────┐
        │ 85 │ 70 │ 92 │ 78 │
        └─────────────────────┘
```

So we can think of:

```text id="c2n6wf"
One Variable
     │
     ▼
One Array
     │
     ▼
Multiple Values
```

This is one of the main reasons arrays are useful.

---

## 8. What Can We Do With an Array?

Once we have an array, we can perform different operations on it.

```text id="p9x5mz"
Array
  │
  ├── Access values
  ├── Add values
  ├── Remove values
  ├── Update values
  ├── Search values
  ├── Filter values
  └── Process values
```

For example:

```text id="v6k3qa"
[85, 70, 92, 78]
      │
      ├── Find a score
      ├── Add a score
      ├── Remove a score
      └── Find the highest score
```

We will learn these operations throughout this module.

---

## 9. Array vs Separate Variables

Compare the two approaches.

### Separate Variables

```text id="n2c7xp"
score1 → 85
score2 → 70
score3 → 92
score4 → 78
```

### Array

```text id="z5m8vr"
scores
   │
   ▼
[85, 70, 92, 78]
```

The array gives us:

```text id="j4q6kw"
One Collection
     │
     ▼
Multiple Related Values
     │
     ▼
Easier to Manage
```

---

## Key Idea

> **An array is an ordered collection that allows a program to store multiple values together.**

Remember:

```text id="a8v3mq"
Array
  │
  ▼
┌────┬────┬────┬────┐
│ 85 │ 70 │ 92 │ 78 │
└────┴────┴────┴────┘
  0    1    2    3
```

An array gives a program a simple way to **store and organize multiple values in one collection**.
