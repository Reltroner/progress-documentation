# Storing Data in JavaScript

A program needs a place to keep data while it is running.

JavaScript provides several ways to store data.

```text
Data
 │
 ├── One Value
 │     └── Variable
 │
 ├── Multiple Values
 │     └── Array
 │
 └── Related Values
       └── Object
````

---

## 1. Storing One Value

A variable can store a single value.

```js
const username = "Alice";
const age = 25;
```

Visualized:

```text
username ──────► "Alice"

age ───────────► 25
```

The variable name gives the program a way to access the value.

```js
console.log(username);
```

Output:

```text
Alice
```

---

## 2. Storing Multiple Values

An array can store multiple values in an ordered collection.

```js
const fruits = ["Apple", "Orange", "Banana"];
```

Visualized:

```text
fruits
  │
  ▼
┌─────────┬──────────┬──────────┐
│  Apple  │  Orange  │  Banana  │
└─────────┴──────────┴──────────┘
    0          1           2
```

Each item has an **index**.

For example:

```js
console.log(fruits[0]);
```

Output:

```text
Apple
```

---

## 3. Storing Related Data

An object can group related information together.

```js
const user = {
  name: "Alice",
  age: 25,
  active: true
};
```

Visualized:

```text
user
 │
 ├── name   ───► "Alice"
 ├── age    ───► 25
 └── active ───► true
```

The properties describe the data.

```js
console.log(user.name);
```

Output:

```text
Alice
```

---

## 4. Choosing a Simple Storage Structure

Different data situations can use different structures.

```text
What are you storing?
        │
        ├── One value
        │      ↓
        │    Variable
        │
        ├── A collection
        │      ↓
        │    Array
        │
        └── Related properties
               ↓
             Object
```

For example:

```text
Username
   ↓
Variable

List of products
   ↓
Array

User profile
   ↓
Object
```

---

## 5. Data Can Be Nested

Structures can also contain other structures.

```js
const user = {
  name: "Alice",
  skills: ["JavaScript", "SQL", "Git"]
};
```

Visualized:

```text
user
 │
 ├── name
 │     └── "Alice"
 │
 └── skills
       │
       ├── JavaScript
       ├── SQL
       └── Git
```

This allows programs to represent more complex information.

---

## 6. Storage Affects How Data Is Used

The way data is stored affects how the program accesses it.

```text
How data is stored
        │
        ▼
How data is accessed
        │
        ▼
How operations are performed
```

For example:

```text
Array
  │
  ▼
Access by index

Object
  │
  ▼
Access by property

Later:
Map
  │
  ▼
Access by key
```

This becomes increasingly important as applications handle more data.

---

## Key Idea

> **JavaScript provides different ways to store data depending on how the data needs to be used.**

The basic choices are:

```text
Variable
   │
   └── One value

Array
   │
   └── Ordered collection

Object
   │
   └── Related properties
```

Choosing how to store data is an important part of programming.

Later in this course, we will learn how **data structures** provide more specialized ways to organize and work with data.

