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

An **array** stores multiple values in an ordered collection.

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
    ▲          ▲           ▲
    │          │           │
 index 0    index 1     index 2
```

### What Is an Index?

An **index** is the position of an item inside an array.

JavaScript arrays start counting from **0**.

```text
┌─────────┬──────────┬──────────┐
│  Apple  │  Orange  │  Banana  │
└─────────┴──────────┴──────────┘
    0          1           2
    ▲
  index
```

So:

```text
fruits[0] → "Apple"
fruits[1] → "Orange"
fruits[2] → "Banana"
```

For example:

```js
console.log(fruits[0]);
```

Output:

```text
Apple
```

> **Index = the position of an item in an array.**

---

## 3. Array vs Object

Both arrays and objects can store multiple pieces of data, but they organize the data differently.

### Array

An array uses **one variable** to hold multiple values.

```js
const fruits = ["Apple", "Orange", "Banana"];
```

Visualized:

```text
       fruits
          │
          ▼
     ┌────┬────┬────┐
     │ A  │ O  │ B  │
     └────┴────┴────┘
       0    1    2
     index index index
```

The values are accessed by their **index**.

```js
fruits[0];
fruits[1];
fruits[2];
```

For this beginner course, think of an array as:

> **One variable → multiple ordered values**

---

### Object

An object uses **named properties** to store related information.

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

Each property has its own name.

```text
name
age
active
```

And each property can store a different type of value.

```text
name   → String
age    → Number
active → Boolean
```

For example:

```js
console.log(user.name);
console.log(user.age);
console.log(user.active);
```

Output:

```text
Alice
25
true
```

For this beginner course, think of an object as:

> **One variable → multiple named properties → each property can hold different kinds of data**

---

## 4. Simple Difference Between Array and Object

The key difference is **how the data is organized and accessed**.

```text
ARRAY
  │
  └── One variable
       │
       └── Multiple ordered values
              │
              └── Access by index
```

Example:

```js
const fruits = ["Apple", "Orange", "Banana"];

fruits[0];
```

```text
fruits[0]
   │
   ▼
"Apple"
```

---

```text
OBJECT
  │
  └── One variable
       │
       └── Multiple named properties
              │
              └── Access by property name
```

Example:

```js
const user = {
  name: "Alice",
  age: 25
};

user.name;
```

```text
user.name
    │
    ▼
"Alice"
```

### Quick Comparison

| Array                                            | Object                                            |
| ------------------------------------------------ | ------------------------------------------------- |
| Stores an ordered collection                     | Stores related information                        |
| Items are accessed by index                      | Properties are accessed by name                   |
| Example: `fruits[0]`                             | Example: `user.name`                              |
| Usually used for lists                           | Usually used for entities/records                 |
| Can contain values of different JavaScript types | Properties can contain different JavaScript types |

> **Important:** JavaScript arrays are not technically required to contain the same data type. They can contain different types of values. However, in real programs, arrays are often used for collections of similar kinds of data because this makes the data easier to understand and work with.

---

## 5. Storing Related Data

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

## 6. Choosing a Simple Storage Structure

Different data situations can use different structures.

```text
What are you storing?
        │
        ├── One value
        │      ↓
        │    Variable
        │
        ├── An ordered collection
        │      ↓
        │    Array
        │
        └── Related information
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

## 7. Data Can Be Nested

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

Here, the object contains an array.

```text
Object
  │
  └── skills
        │
        ▼
      Array
        │
        ├── JavaScript
        ├── SQL
        └── Git
```

This allows programs to represent more complex information.

---

## 8. Storage Affects How Data Is Used

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
       └── Access by index

Object
   │
   └── Related properties
       └── Access by property name
```

Choosing how to store data is an important part of programming.

As programs become larger, we need more specialized ways to organize and work with data.

That is where **data structures** become important.

