# What Is an Algorithm?

An **algorithm** is a **step-by-step process for solving a problem or completing a task**.

In simple terms:

> **An algorithm tells a program what steps to take to get a result.**

```text
Problem
   │
   ▼
Algorithm
   │
   ├── Step 1
   ├── Step 2
   ├── Step 3
   └── ...
   │
   ▼
Result
````

---

## 1. Algorithms Are Step-by-Step Instructions

Think about making a cup of coffee.

```text
Start
  │
  ▼
Boil Water
  │
  ▼
Add Coffee
  │
  ▼
Add Hot Water
  │
  ▼
Mix
  │
  ▼
Coffee Ready
```

Each step contributes to the final result.

This is the basic idea of an algorithm.

---

## 2. Algorithms Solve Problems

Programs use algorithms to perform tasks.

For example, suppose we want to find a user's name.

```text
Problem
   │
   ▼
Find "Alice"
   │
   ▼
Search the data
   │
   ▼
Check each value
   │
   ▼
Found "Alice"
```

The steps used to find the user form an **algorithm**.

```text
Data
 │
 ▼
Algorithm
 │
 ▼
Search
 │
 ▼
Result
```

---

## 3. A Simple JavaScript Algorithm

Consider this program:

```js
const numbers = [10, 20, 30];
const target = 20;

for (const number of numbers) {
  if (number === target) {
    console.log("Found");
    break;
  }
}
```

The algorithm can be described as:

```text
Start
  │
  ▼
Take the first number
  │
  ▼
Is it the target?
  │
 ┌┴───────────┐
 │            │
Yes           No
 │            │
 ▼            ▼
Found      Take the
           next number
                │
                └──────► Repeat
```

The JavaScript code is the **implementation** of the algorithm.

---

## 4. Algorithm vs Code

An algorithm describes the **steps**.

Code describes those steps in a **programming language**.

```text
Problem
   │
   ▼
Algorithm
   │
   ▼
JavaScript Code
   │
   ▼
Program Result
```

For example:

```text
Algorithm:

1. Start with the first number.
2. Compare it with the target.
3. If it matches, stop.
4. Otherwise, check the next number.
5. Repeat until the value is found.
```

Then we can implement those steps using JavaScript.

```js
const numbers = [10, 20, 30];
const target = 20;
```

The algorithm is the **idea and sequence of steps**.

The code is the **implementation of that idea**.

---

## 5. The Same Problem Can Have Different Algorithms

A problem does not always have only one solution.

For example:

```text
Problem
   │
   ▼
Find a value
   │
   ├── Algorithm A
   │      └── Check values one by one
   │
   └── Algorithm B
          └── Use a faster search strategy
```

Both algorithms may solve the same problem.

However, they may have different:

* Number of steps
* Speed
* Memory usage
* Requirements

This is why algorithm choice matters.

---

## 6. Algorithms Work With Data

Algorithms usually operate on data.

```text
        DATA
          │
          ▼
      ALGORITHM
          │
          ▼
       PROCESS
          │
          ▼
        RESULT
```

For example:

```text
Products
   │
   ▼
Sorting Algorithm
   │
   ▼
Products ordered by price
```

Or:

```text
Users
   │
   ▼
Search Algorithm
   │
   ▼
Requested User
```

---

## 7. Algorithm and Data Structure

Data structures and algorithms work together.

```text
             DATA
               │
               ▼
       ┌───────────────┐
       │ Data Structure│
       └───────────────┘
               │
               ▼
       ┌───────────────┐
       │   Algorithm   │
       └───────────────┘
               │
               ▼
            Result
```

A **data structure** determines how data is organized.

An **algorithm** determines the steps used to work with that data.

```text
Data Structure
      │
      └── How data is organized

Algorithm
      │
      └── How data is processed
```

Together, they help a program solve problems effectively.

---

## Key Idea

> **An algorithm is a step-by-step process for solving a problem or completing a task.**

The basic relationship is:

```text
Problem
   │
   ▼
Algorithm
   │
   ▼
Implementation
   │
   ▼
Result
```

And when working with data:

```text
Data
 │
 ▼
Data Structure
 │
 ▼
Algorithm
 │
 ▼
Result
```

The goal of learning algorithms is not simply to memorize steps.

It is to learn how to **design, understand, compare, and choose steps that effectively solve a problem**.

