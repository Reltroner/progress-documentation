# What Is Data?

Data is **information that a program can store, read, change, and use**.

In programming, data can represent almost anything:

- A user's name
- A product price
- A login status
- A list of products
- A score
- A date
- A customer record

---

## 1. Data in Everyday Life

Think about the information used by an online store:

```text
Online Store
│
├── Product Name
├── Price
├── Stock
├── Category
└── Availability
````

All of these are **data**.

A program uses this data to perform operations.

```text
        DATA
          │
          ▼
     ┌───────────┐
     │  Program  │
     └───────────┘
          │
     ┌────┼────┐
     ▼    ▼    ▼
   Read  Change Use
```

---

## 2. Data Can Have Different Forms

Different information can be represented using different types of data.

```text
Data
│
├── Text
│   └── "Alice"
│
├── Number
│   └── 250
│
├── Boolean
│   └── true
│
├── Array
│   └── ["Apple", "Orange", "Banana"]
│
└── Object
    └── { name: "Alice", age: 25 }
```

JavaScript provides different ways to represent these values.

```js
const name = "Alice";
const age = 25;
const isActive = true;
```

Here:

```text
name      → Text
age       → Number
isActive  → Boolean
```

---

## 3. A Program Works With Data

A simple program usually performs operations on data.

```text
          DATA
            │
            ▼
     ┌──────────────┐
     │   PROGRAM    │
     └──────────────┘
            │
     ┌──────┼──────┐
     ▼      ▼      ▼
   READ   CHANGE   USE
     │      │      │
     └──────┼──────┘
            ▼
          RESULT
```

For example:

```js
let score = 80;

score = score + 10;

console.log(score);
```

The program:

```text
Initial Data
    │
    ▼
score = 80
    │
    ▼
Change the data
    │
    ▼
score = 90
    │
    ▼
Use the result
    │
    ▼
Console Output
```

---

## 4. One Value vs Many Values

Sometimes a program only needs to store one value.

```js
const username = "Alice";
```

But real applications often need to work with many values.

```js
const usernames = [
  "Alice",
  "Bob",
  "Charlie"
];
```

Now the data looks like:

```text
username
   │
   ▼
"Alice"


usernames
   │
   ▼
┌─────────┬─────────┬───────────┐
│  Alice  │   Bob   │  Charlie  │
└─────────┴─────────┴───────────┘
```

This is where **data structures** become important.

---

## 5. Why Does Data Structure Matter?

Imagine you have 1,000,000 users.

You need to find one user quickly.

```text
1,000,000 Users
       │
       ▼
     Search
       │
       ▼
"Find user #829374"
```

How the data is organized can affect how efficiently the program finds that user.

```text
Data
 │
 ▼
How is it organized?
 │
 ▼
Data Structure
 │
 ▼
How can we access it?
 │
 ▼
Program Performance
```

This is one of the main reasons we study **Data Structures & Algorithms**.

---

## Key Idea

> **Data is information that a program stores and works with.**

As programs become larger, we need better ways to:

* Store data
* Access data
* Search data
* Update data
* Organize data
* Process data

These needs lead us to **data structures and algorithms**.

```text
DATA
 │
 ├── Store
 ├── Access
 ├── Search
 ├── Update
 └── Process
        │
        ▼
Data Structures + Algorithms
```

### Remember

**Data = the information.**

**Data Structure = how the information is organized.**

**Algorithm = the steps used to work with the information.**
