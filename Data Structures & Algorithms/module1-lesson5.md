# What Is a Data Structure?

A **data structure** is a way to **organize and store data** so a program can work with it.

Think of it as a container with a specific way of organizing information.

```text
Data
 │
 ▼
┌─────────────────────┐
│    Data Structure   │
│                     │
│  Organize the data  │
└─────────────────────┘
 │
 ├── Store
 ├── Access
 ├── Search
 ├── Update
 └── Process
````

---

## 1. Why Do We Need Data Structures?

A program may need to work with many values.

For example:

```text
1,000 Users
      │
      ▼
   Program
      │
      ├── Find a user
      ├── Add a user
      ├── Remove a user
      └── Update a user
```

The program needs a way to organize those users.

```text
Many Values
     │
     ▼
Organize the Data
     │
     ▼
Data Structure
```

Without a suitable structure, working with large or complex data can become harder.

---

## 2. Data Structures Organize Data

Different structures organize data in different ways.

```text
             DATA
              │
      ┌───────┼────────┐
      ▼       ▼        ▼
   Array    Object     Map
      │       │        │
      ▼       ▼        ▼
  Ordered   Related   Key-based
  values    data      data
```

For example, an array organizes values by position:

```text
Array
 │
 ▼
┌────┬────┬────┬────┐
│ A  │ B  │ C  │ D  │
└────┴────┴────┴────┘
  0    1    2    3
```

An object organizes related values using property names:

```text
Object
 │
 ├── name
 ├── age
 └── active
```

The structure affects how the program works with the data.

---

## 3. A Data Structure Is More Than Storage

A data structure is not simply a place to put values.

It also determines **how the data can be organized and accessed**.

```text
Data Structure
      │
      ├── How data is organized
      │
      ├── How data is accessed
      │
      ├── How data is added
      │
      ├── How data is removed
      │
      └── How data is processed
```

For example:

```text
Array
 │
 └── Access by index

Object
 │
 └── Access by property

Map
 │
 └── Access by key
```

---

## 4. Choosing a Data Structure

The best data structure depends on what the program needs to do.

```text
What does the program need?
          │
          ▼
   ┌───────────────┐
   │ Store data    │
   │ Search data   │
   │ Update data   │
   │ Process data  │
   └───────────────┘
          │
          ▼
Choose a suitable
Data Structure
```

For example:

```text
Need an ordered list?
        ↓
      Array

Need related properties?
        ↓
      Object

Need key-based lookup?
        ↓
       Map
```

Later, we will learn structures designed for other needs:

```text
Stack
Queue
Linked List
Tree
Graph
```

---

## 5. Data Structure vs Data

It is important to distinguish the **data** from the **structure** used to organize it.

```text
DATA
 │
 └── "Alice"
     25
     true
```

The structure determines how multiple pieces of data are organized.

```text
DATA
 │
 ▼
DATA STRUCTURE
 │
 ▼
How the program works with the data
```

For example:

```js
const users = ["Alice", "Bob", "Charlie"];
```

Here:

```text
"Alice"
"Bob"
"Charlie"
     │
     ▼
   DATA
     │
     ▼
   Array
     │
     ▼
Data Structure
```

---

## Key Idea

> **A data structure is a way to organize and store data so a program can work with it effectively.**

The relationship is:

```text
        DATA
          │
          ▼
   DATA STRUCTURE
          │
          ▼
 ┌────────┼─────────┐
 ▼        ▼         ▼
Access   Search   Process
```

Different problems may require different data structures.

The important question is not:

> "Which data structure should I memorize?"

Instead, ask:

> **"How does my program need to work with this data?"**

That question will help you choose an appropriate data structure.

