# From Problem to Solution

Programming starts with a **problem**.

Before writing code, we need to understand what the program is expected to do.

```text
Problem
   │
   ▼
Understand the Problem
   │
   ▼
Plan the Solution
   │
   ▼
Write the Algorithm
   │
   ▼
Write the Code
   │
   ▼
Test the Result
````

---

## 1. Start With the Problem

First, identify what needs to be solved.

For example:

> "Find the highest score from a list of scores."

```text
Problem
   │
   ▼
Find the highest score
   │
   ▼
Input:
[70, 85, 92, 78]
   │
   ▼
Expected Output:
92
```

Do not start coding immediately.

First understand the problem.

---

## 2. Identify the Input

The **input** is the data the program receives.

```text
INPUT
  │
  ▼
[70, 85, 92, 78]
```

Ask:

* What data do we receive?
* What type of data is it?
* How many values might there be?

For this problem:

```text
Input
  │
  └── A collection of scores
```

---

## 3. Identify the Expected Output

The **output** is the result the program should produce.

```text
Input
  │
  ▼
[70, 85, 92, 78]
  │
  ▼
Program
  │
  ▼
Output
  │
  ▼
92
```

Clearly defining the output helps us understand what the algorithm needs to accomplish.

---

## 4. Break the Problem Into Steps

A problem can often be easier to solve when broken into smaller steps.

For example:

```text
Find the highest score
        │
        ▼
Start with the first score
        │
        ▼
Compare it with the next score
        │
        ▼
Is the next score higher?
     ┌──┴──┐
    Yes    No
     │      │
     ▼      │
Update      │
highest     │
     │      │
     └──┬───┘
        ▼
Continue until the end
        │
        ▼
Return the highest score
```

These steps form the basis of an algorithm.

---

## 5. Write the Algorithm Before the Code

We can describe the solution without using JavaScript first.

```text
Algorithm:

1. Take the first score as the highest.
2. Look at the next score.
3. If it is higher, update the highest score.
4. Continue through all scores.
5. Return the highest score.
```

Visualized:

```text
Scores
  │
  ▼
Start
  │
  ▼
Compare values
  │
  ▼
Keep the highest
  │
  ▼
Repeat
  │
  ▼
Return result
```

This makes the solution easier to understand before implementation.

---

## 6. Implement the Solution

Once the steps are clear, translate them into JavaScript.

```js
const scores = [70, 85, 92, 78];

let highest = scores[0];

for (const score of scores) {
  if (score > highest) {
    highest = score;
  }
}

console.log(highest);
```

Output:

```text
92
```

The complete flow is:

```text
Problem
   │
   ▼
"Find the highest score"
   │
   ▼
Input
   │
   ▼
[70, 85, 92, 78]
   │
   ▼
Algorithm
   │
   ▼
Compare each score
   │
   ▼
JavaScript Code
   │
   ▼
Output
   │
   ▼
92
```

---

## 7. Test the Solution

A solution should be tested with different inputs.

```text
Normal Input
    │
    ▼
[70, 85, 92, 78]
    │
    ▼
92
```

Try another input:

```text
[50, 40, 30]
      │
      ▼
    50
```

And:

```text
[100]
  │
  ▼
100
```

Testing helps us check whether the solution works correctly.

---

## 8. The Basic Problem-Solving Cycle

A simple programming workflow looks like this:

```text
       ┌──────────────────────┐
       │      Understand      │
       │      the Problem     │
       └──────────┬───────────┘
                  ▼
       ┌──────────────────────┐
       │    Identify Input    │
       │      & Output        │
       └──────────┬───────────┘
                  ▼
       ┌──────────────────────┐
       │    Plan the Steps    │
       └──────────┬───────────┘
                  ▼
       ┌──────────────────────┐
       │   Write Algorithm    │
       └──────────┬───────────┘
                  ▼
       ┌──────────────────────┐
       │   Write JavaScript   │
       └──────────┬───────────┘
                  ▼
       ┌──────────────────────┐
       │   Test the Solution  │
       └──────────┬───────────┘
                  │
                  └──────────► Improve if needed
```

---

## Key Idea

> **Good problem solving starts with understanding the problem before writing code.**

The basic flow is:

```text
Problem
   ↓
Input + Output
   ↓
Steps
   ↓
Algorithm
   ↓
JavaScript
   ↓
Test
   ↓
Result
```

The code is only one part of the solution.

**Understanding the problem and designing the steps come first.**
