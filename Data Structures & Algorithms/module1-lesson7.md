# Data Structure vs Algorithm

**Data structures** and **algorithms** are closely related, but they solve different parts of a problem.

```text
Data Structure
      │
      └── How data is organized

Algorithm
      │
      └── How data is processed
````

A simple way to remember:

> **Data Structure = how data is organized.**
> **Algorithm = the steps used to work with the data.**

---

## 1. Data Structure

A data structure determines **how data is organized and stored**.

For example, an array stores values in an ordered collection:

```text id="5rkg5v"
Array
  │
  ▼
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │
└────┴────┴────┴────┘
  0    1    2    3
```

The structure tells us how the data is arranged.

Other examples include:

```text id="5wq2ai"
Data Structures
│
├── Array
├── Object
├── Map
├── Stack
├── Queue
├── Linked List
├── Tree
└── Graph
```

---

## 2. Algorithm

An algorithm determines **the steps used to solve a problem or process data**.

For example, to find `30` in an array:

```text id="wzzx1k"
Array
 │
 ▼
10 → 20 → 30 → 40
 │     │     │
 ▼     ▼     ▼
Check Check Check
 │     │     │
 No    No   YES
             │
             ▼
           Found
```

The sequence of checking the values is the **algorithm**.

---

## 3. They Work Together

A program often uses both a data structure and an algorithm.

```text id="a9fd9k"
       DATA
         │
         ▼
┌─────────────────┐
│  Data Structure │
│                 │
│ How data is     │
│ organized       │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│    Algorithm    │
│                 │
│ How data is     │
│ processed       │
└─────────────────┘
         │
         ▼
       RESULT
```

For example:

```text id="h0o2u9"
User Data
    │
    ▼
  Array
    │
    ▼
Search Algorithm
    │
    ▼
Find User
```

Here:

```text
Array
  → Data Structure

Search
  → Algorithm
```

---

## 4. A Simple Real-World Analogy

Imagine a library.

```text id="6v0sqs"
Books
  │
  ▼
How are books organized?
  │
  ▼
Shelves
  │
  ▼
How do we find a book?
  │
  ▼
Search Process
```

The **shelves** are similar to a data structure.

The **search process** is similar to an algorithm.

```text
Library Shelves
      │
      └── Organization
            ↓
       Data Structure


Finding a Book
      │
      └── Steps
            ↓
         Algorithm
```

---

## 5. Changing the Data Structure

The same type of data can be organized differently.

```text id="k6f2n7"
              User Data
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
      Array     Object      Map
        │         │         │
        ▼         ▼         ▼
   Different ways to
   organize the data
```

Changing the data structure can change how the program accesses the data.

---

## 6. Changing the Algorithm

The same problem can also be solved using different algorithms.

```text id="q9m5se"
              Find User
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
 Linear Search        Binary Search
        │                   │
        ▼                   ▼
 Check one by one     Reduce the search
                      range repeatedly
```

Both are search algorithms.

The difference is **how they solve the search problem**.

---

## 7. The Complete Picture

When solving a programming problem, think about both questions:

```text id="a2ik4m"
            PROBLEM
               │
       ┌───────┴────────┐
       ▼                ▼
How should          What steps
data be organized?  should we take?
       │                │
       ▼                ▼
Data Structure       Algorithm
       │                │
       └───────┬────────┘
               ▼
             RESULT
```

For example:

```text id="r2w7cg"
Problem:
Find a product by ID

       │
       ▼

Data Structure:
Map

       │
       ▼

Algorithm:
Look up the product using its key

       │
       ▼

Result:
Product found
```

---

## Quick Comparison

| Data Structure                    | Algorithm                                       |
| --------------------------------- | ----------------------------------------------- |
| Organizes data                    | Processes data                                  |
| Defines how data is stored        | Defines the steps to solve a problem            |
| Examples: Array, Map, Stack, Tree | Examples: Linear Search, Binary Search, Sorting |
| Focuses on data organization      | Focuses on problem-solving steps                |

---

## Key Idea

> **A data structure organizes the data. An algorithm defines the steps used to work with that data.**

Think of them as:

```text id="r3t6ac"
DATA STRUCTURE
      │
      │  Organizes
      ▼
     DATA
      │
      │  Processed by
      ▼
   ALGORITHM
      │
      ▼
    RESULT
```

Good software often requires choosing **both** an appropriate data structure and an appropriate algorithm.
