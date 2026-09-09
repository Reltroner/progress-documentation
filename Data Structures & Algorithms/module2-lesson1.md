# Why We Need Collections

Programs often need to work with **more than one value**.

For example, an online store may have many products:

```text id="n8y2fk"
Laptop
Mouse
Keyboard
Monitor
Headset
```

Storing every value separately can quickly become difficult to manage.

This is why programs use **collections**.

```text id="x3m7qa"
Many Values
     │
     ▼
┌───────────────┐
│   Collection  │
└───────────────┘
     │
     ▼
Organized Data
```

---

## Lesson Objectives

By the end of this lesson, you should be able to:

* **Explain** why programs need collections.
* **Identify** situations where multiple values need to be managed together.
* **Understand** how collections organize related data.
* **Recognize** why storing many values separately can become difficult.
* **Identify** arrays as one way to store a collection of values in JavaScript.

---

## 1. Programs Work With Many Values

A real program rarely works with only one value.

For example, an e-commerce application may need to manage:

```text id="5u7g9r"
Products
   │
   ├── Laptop
   ├── Mouse
   ├── Keyboard
   ├── Monitor
   └── Headset
```

A school application may manage:

```text id="q1b4hz"
Student Scores
   │
   ├── 85
   ├── 70
   ├── 92
   ├── 78
   └── 88
```

A social media application may manage:

```text id="x9f3jk"
Users
   │
   ├── Alex
   ├── Sarah
   ├── John
   └── Maria
```

These are all examples of **multiple related values**.

---

## 2. The Problem With Separate Variables

One way to store multiple values is to create separate variables.

```js id="w8x2pk"
const product1 = "Laptop";
const product2 = "Mouse";
const product3 = "Keyboard";
const product4 = "Monitor";
```

Visualized:

```text id="j7v4ps"
product1 → Laptop

product2 → Mouse

product3 → Keyboard

product4 → Monitor
```

This works for a few values.

But imagine having **100 products**.

```text id="h5d8qa"
product1
product2
product3
product4
...
product100
```

This becomes difficult to manage.

```text id="3kq7xm"
Many Values
     │
     ▼
Many Separate Variables
     │
     ▼
Harder to Manage
```

---

## 3. Group Related Values Together

Instead of storing each value separately, we can group related values into a **collection**.

```text id="z6p4tn"
             Products
                 │
        ┌────────┼────────┐
        ▼        ▼        ▼
     Laptop    Mouse   Keyboard
                 │
                 ▼
              Collection
```

In JavaScript, an array can be used:

```js id="b5v1qd"
const products = [
  "Laptop",
  "Mouse",
  "Keyboard",
  "Monitor"
];
```

Now the values are grouped together:

```text id="r2k9wf"
products
   │
   ├── Laptop
   ├── Mouse
   ├── Keyboard
   └── Monitor
```

---

## 4. What Is a Collection?

A **collection** is a group of related values managed together.

```text id="m8c2rx"
Collection
    │
    ├── Value
    ├── Value
    ├── Value
    └── Value
```

Examples:

```text id="p3h7vz"
Collection of Products
[ Laptop, Mouse, Keyboard ]

Collection of Scores
[ 85, 70, 92, 78 ]

Collection of Names
[ Alex, Sarah, John ]
```

The values belong to the same general group.

---

## 5. Collections Make Data Easier to Work With

A collection allows a program to work with many values as one group.

```text id="u9q5wb"
Without Collection

Laptop
Mouse
Keyboard
Monitor
   │
   ▼
Separate Values


With Collection

[ Laptop, Mouse, Keyboard, Monitor ]
                │
                ▼
            One Group
```

This makes common operations easier.

For example:

```text id="v6f1kc"
Collection
    │
    ├── Add a value
    ├── Remove a value
    ├── Find a value
    ├── Update a value
    └── Process values
```

These operations will be explored throughout this module.

---

## 6. Example: Student Scores

Imagine a program needs to manage several student scores.

Without a collection:

```js id="p8q2lm"
const score1 = 85;
const score2 = 70;
const score3 = 92;
const score4 = 78;
```

Visualized:

```text id="x1c7ha"
score1 → 85
score2 → 70
score3 → 92
score4 → 78
```

With an array:

```js id="n4y8zr"
const scores = [85, 70, 92, 78];
```

Visualized:

```text id="k2w6ps"
scores
  │
  ├── 85
  ├── 70
  ├── 92
  └── 78
```

The scores are now managed as one collection.

---

## 7. Collections Help With Repeated Operations

Suppose we want to display every score.

With separate variables:

```text id="a7r3mx"
score1
score2
score3
score4
...
```

As the number of values grows, managing them becomes harder.

With a collection:

```text id="c9v5td"
[85, 70, 92, 78]
        │
        ▼
   Process each value
        │
        ├── 85
        ├── 70
        ├── 92
        └── 78
```

This allows programs to perform operations on the collection.

For example:

```js id="e6t1qz"
const scores = [85, 70, 92, 78];

for (const score of scores) {
  console.log(score);
}
```

Output:

```text id="j4p8sw"
85
70
92
78
```

---

## 8. Common Examples of Collections

Collections appear everywhere in software.

```text id="q8m3vx"
E-Commerce
    ↓
Products

School System
    ↓
Students

Banking System
    ↓
Transactions

Social Media
    ↓
Users

Video Platform
    ↓
Videos

Task Management
    ↓
Tasks
```

The specific data changes, but the idea is the same:

```text id="t5k7nc"
Many Related Values
        ↓
     Collection
        ↓
Easy to Manage
```

---

## 9. Choosing a Collection

Different problems may require different ways of organizing data.

For example:

```text id="w3f9qa"
Ordered Values
      ↓
    Array

Key-Based Data
      ↓
   Object / Map

First-In, First-Out
      ↓
    Queue

Last-In, First-Out
      ↓
    Stack
```

In this module, we will start with **arrays** because they are one of the most common ways to work with collections in JavaScript.

---

## 10. From Many Values to an Array

The basic idea is:

```text id="r7n2km"
Many Related Values
        │
        ▼
     Collection
        │
        ▼
       Array
        │
        ▼
[85, 70, 92, 78]
```

JavaScript example:

```js id="h2v6ps"
const scores = [85, 70, 92, 78];
```

Now the program can work with the scores as a group.

---

## Key Idea

> **Collections allow programs to organize and work with multiple related values as a group.**

Remember:

```text id="m4x8cz"
Many Values
    ↓
Collection
    ↓
Organized Data
    ↓
Easier to Work With
```

In JavaScript, **arrays** are a common way to store collections of values.
