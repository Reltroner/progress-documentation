# Writing Simple Pseudocode

Before writing JavaScript code, we can describe the solution using **simple pseudocode**.

Pseudocode is a way to describe an algorithm using **simple, human-readable steps**.

```text id="5r8v2m"
Problem
   │
   ▼
Break Into Steps
   │
   ▼
Pseudocode
   │
   ▼
JavaScript Code
```

Pseudocode helps us focus on the **logic** before thinking about programming syntax.

---

## Lesson Objectives

By the end of this lesson, you should be able to:

* **Explain** what pseudocode is.
* **Write** simple pseudocode for a programming problem.
* **Use** simple steps to describe an algorithm.
* **Translate** pseudocode into JavaScript.
* **Use** pseudocode to plan a solution before coding.

---

## 1. What Is Pseudocode?

Pseudocode is a **simple description of an algorithm**.

It looks like code, but it does not follow the exact syntax of a programming language.

```text id="f7g1j8"
Pseudocode
     │
     ├── Easy to read
     ├── Focuses on logic
     └── Not tied to one programming language
```

For example:

```text id="g0x5lz"
START
  ↓
Get a list of scores
  ↓
Find the highest score
  ↓
Return the highest score
  ↓
END
```

This is pseudocode.

It describes **what the program should do**, without worrying about JavaScript syntax.

---

## 2. Why Use Pseudocode?

Imagine you immediately start writing code:

```js id="4tw2la"
const scores = [85, 70, 92, 78];

let highest = scores[0];

for (const score of scores) {
  if (score > highest) {
    highest = score;
  }
}
```

You need to think about both:

```text id="q8z3mi"
Problem Logic
     +
JavaScript Syntax
```

Pseudocode separates them:

```text id="4j3q7y"
Problem
   ↓
Logic
   ↓
Pseudocode
   ↓
JavaScript
```

This allows you to solve the **logic first**.

---

## 3. Example Problem

Consider this problem:

> **Find the highest score from a list.**

Input:

```text id="3j5x8h"
[85, 70, 92, 78]
```

Output:

```text id="4gjz0k"
92
```

First, think about the steps:

```text id="j0q6g7"
Take the first score
        ↓
Set it as the highest
        ↓
Check the next score
        ↓
Compare it with the highest
        ↓
Update if necessary
        ↓
Repeat
        ↓
Return the highest
```

Now we can turn those steps into pseudocode.

---

## 4. Simple Pseudocode

```text id="v8c2k5"
START

Get the scores

Set highest to the first score

For each score:
    If the score is greater than highest:
        Set highest to the score

Return highest

END
```

Notice that this is not JavaScript.

There are no:

* `const`
* `let`
* `{ }`
* JavaScript-specific syntax

The focus is only on the **logic**.

---

## 5. Visualizing the Pseudocode

The pseudocode can be represented as:

```text id="g8v0a3"
              START
                │
                ▼
         Get the scores
                │
                ▼
      Set first score as
             highest
                │
                ▼
         Get next score
                │
                ▼
       Compare with highest
                │
                ▼
          Is it greater?
           │          │
          YES         NO
           │           │
           ▼           │
      Update highest   │
           │           │
           └─────┬─────┘
                 ▼
          More scores?
           │          │
          YES         NO
           │           │
           └─────┐     ▼
                 │  Return highest
                 │     │
                 └─────┘
                       │
                       ▼
                      END
```

Pseudocode and diagrams describe the same solution.

---

## 6. Pseudocode vs JavaScript

The same logic can later be written in JavaScript.

### Pseudocode

```text id="t8w6f2"
Set highest to the first score

For each score:
    If score is greater than highest:
        Update highest

Return highest
```

### JavaScript

```js id="q9x7y1"
const scores = [85, 70, 92, 78];

let highest = scores[0];

for (const score of scores) {
  if (score > highest) {
    highest = score;
  }
}

console.log(highest);
```

The idea is the same:

```text id="0x3f7n"
Pseudocode
    │
    │  Same logic
    ▼
JavaScript
```

Only the **syntax** changes.

---

## 7. Common Pseudocode Words

Simple pseudocode often uses words such as:

```text id="m4j8q2"
START
END
GET
SET
IF
ELSE
FOR EACH
REPEAT
RETURN
```

Example:

```text id="y6p3q9"
START

GET user

IF user exists:
    RETURN user

ELSE:
    RETURN "User not found"

END
```

These words make the logic easy to understand.

---

## 8. Keep Pseudocode Simple

Pseudocode does not need to be complicated.

Avoid writing unnecessary details:

```text id="2b6y8v"
❌ Too detailed

Declare a variable called highest
and assign the value at index zero
of the scores array using JavaScript
array syntax...
```

Instead:

```text id="7x4n2c"
✓ Simple

Set highest to the first score
```

The goal is:

```text id="9v3k5w"
Clear Logic
    +
Simple Steps
    =
Useful Pseudocode
```

---

## 9. From Problem to Code

A complete workflow looks like this:

```text id="4s8m1q"
             PROBLEM
                │
                ▼
       Understand the problem
                │
                ▼
        Break into small steps
                │
                ▼
            PSEUDOCODE
                │
                ▼
        Implement in JavaScript
                │
                ▼
              TEST
                │
                ▼
             RESULT
```

For example:

```text id="n7c2x5"
Problem
Find highest score
      ↓
Input
[85, 70, 92, 78]
      ↓
Pseudocode
Compare each score
      ↓
JavaScript
Implement the algorithm
      ↓
Output
92
```

---

## Key Idea

> **Pseudocode describes the logic of a solution before we write the actual code.**

Remember:

```text id="w2f9k6"
Problem
   ↓
Steps
   ↓
Pseudocode
   ↓
JavaScript
   ↓
Result
```

**Keep pseudocode simple, clear, and focused on the steps of the solution.**
