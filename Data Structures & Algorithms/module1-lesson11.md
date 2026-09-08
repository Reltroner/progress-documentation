# Understanding Input and Output

## Lesson Objectives

By the end of this lesson, you should be able to:

* **Identify** the input of a programming problem.
* **Identify** the expected output.
* **Distinguish** between input, process, and output.
* **Describe** a simple problem using the `Input → Process → Output` pattern.
* **Translate** a simple problem into basic JavaScript input and output.

---

Every program works with **input** and produces **output**.

A simple way to think about a program is:

```text
Input
  │
  ▼
┌─────────────┐
│   Program   │
└─────────────┘
  │
  ▼
Output
```

The program receives data, processes it, and produces a result.

---

## 1. What Is Input?

**Input** is the data given to a program.

```text
Input
  │
  ├── Number
  ├── Text
  ├── Boolean
  ├── Array
  └── Object
```

For example:

```js
const scores = [85, 70, 92, 78];
```

The array can be used as input for a program that needs to process scores.

```text
Input

[85, 70, 92, 78]
        │
        ▼
     Program
```

---

## 2. What Is Output?

**Output** is the result produced by a program.

For example, if the program finds the highest score:

```text
Input
[85, 70, 92, 78]
        │
        ▼
   Find highest
        │
        ▼
Output
   92
```

In JavaScript:

```js
console.log(92);
```

Output:

```text
92
```

---

## 3. Input → Process → Output

Most simple programming problems can be represented as:

```text
┌─────────┐
│  Input  │
└────┬────┘
     │
     ▼
┌─────────┐
│ Process │
└────┬────┘
     │
     ▼
┌─────────┐
│ Output  │
└─────────┘
```

Example:

```text
Input
[85, 70, 92, 78]
        │
        ▼
Compare the scores
        │
        ▼
Find the highest
        │
        ▼
Output
92
```

---

## 4. Input Can Have Multiple Values

Input does not have to be a single value.

It can be a collection of values:

```js
const products = [
  "Laptop",
  "Mouse",
  "Keyboard"
];
```

Visualized:

```text
Input
   │
   ▼
┌─────────────────────┐
│ Laptop              │
│ Mouse               │
│ Keyboard            │
└─────────────────────┘
```

The program can then process these values.

---

## 5. Output Can Have Different Forms

Output can also contain different types of data.

```text
Output
  │
  ├── Number
  │
  ├── Text
  │
  ├── Boolean
  │
  ├── Array
  │
  └── Object
```

For example:

### Number

```js
console.log(92);
```

```text
92
```

### Text

```js
console.log("Product found");
```

```text
Product found
```

### Boolean

```js
console.log(true);
```

```text
true
```

### Array

```js
console.log(["Apple", "Orange", "Banana"]);
```

```text
["Apple", "Orange", "Banana"]
```

---

## 6. Example: Find the Highest Score

Let's connect input and output to a real problem.

### Problem

> Find the highest score from a list of scores.

```text
Input
   │
   ▼
[85, 70, 92, 78]
   │
   ▼
Process
   │
   ├── Compare 85
   ├── Compare 70
   ├── Compare 92
   └── Compare 78
   │
   ▼
Output
   │
   ▼
92
```

The input and output are different:

```text
INPUT
[85, 70, 92, 78]

        ↓

PROCESS
Find the highest value

        ↓

OUTPUT
92
```

---

## 7. Why Input and Output Matter

Before solving a problem, clearly identify:

```text
What data do I receive?
          │
          ▼
        INPUT
          │
          ▼
What should my program do?
          │
          ▼
       PROCESS
          │
          ▼
What result should I produce?
          │
          ▼
        OUTPUT
```

If the input and output are unclear, it is difficult to design the correct solution.

---

## 8. A Simple Problem-Solving Pattern

When you receive a programming problem, ask three questions:

```text
1. What is the INPUT?
          │
          ▼
2. What PROCESS is needed?
          │
          ▼
3. What is the OUTPUT?
```

For example:

```text
Problem:
"Find the highest score."

        │
        ▼

INPUT:
[85, 70, 92, 78]

        │
        ▼

PROCESS:
Compare the scores

        │
        ▼

OUTPUT:
92
```

This simple pattern helps turn a problem into a solution.

---

## Key Idea

> **Input is the data a program receives. Output is the result a program produces.**

Remember:

```text
INPUT
  ↓
PROCESS
  ↓
OUTPUT
```

Before writing code, make sure you understand **what goes in** and **what should come out**.
