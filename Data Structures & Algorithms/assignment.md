# Assignment — Solve a Simple Data Problem

## Objective

In this assignment, you will practice solving a simple data problem from start to finish.

You will:

```text
Analyze the Problem
       ↓
Identify Input & Output
       ↓
Break the Problem Into Steps
       ↓
Write Simple Pseudocode
       ↓
Implement in JavaScript
       ↓
Test the Solution
```

---

## Scenario

You are building a simple **student score analyzer**.

The program receives a list of student scores and needs to find the **highest score**.

Example input:

```js
const scores = [85, 70, 92, 78];
```

Expected output:

```text
92
```

---

## Task 1 — Analyze the Problem

Write a short description of the problem.

Answer:

* What problem does the program need to solve?
* What data does the program receive?
* What result should the program produce?

Use this structure:

```text
Problem:
...

Input:
...

Output:
...
```

Example:

```text
Problem:
Find the highest score from a list of student scores.

Input:
A list of student scores.

Output:
The highest score.
```

---

## Task 2 — Define the Input and Output

Identify the input and output for this problem.

### Input

Use:

```js
const scores = [85, 70, 92, 78];
```

Visualize the input:

```text
INPUT

[85, 70, 92, 78]
```

### Output

The expected result is:

```text
OUTPUT

92
```

Complete:

```text
Input:
____________________________

Output:
____________________________
```

---

## Task 3 — Break the Problem Into Steps

Break the problem into small steps.

Think about:

```text
What should happen first?
        ↓
What should happen next?
        ↓
What should happen after that?
        ↓
When is the problem finished?
```

Write at least **5 steps**.

For example:

```text
1. Take the first score.
2. Set it as the highest score.
3. Check the next score.
4. Compare it with the highest score.
5. Update the highest score if necessary.
6. Repeat until all scores are checked.
7. Return the highest score.
```

---

## Task 4 — Write Simple Pseudocode

Convert your steps into simple pseudocode.

Use the following format:

```text
START

Get the scores

Set highest to the first score

For each score:
    If the score is greater than highest:
        Update highest

Return highest

END
```

You may improve the pseudocode if you have a different valid approach.

---

## Task 5 — Implement the Solution in JavaScript

Create a JavaScript file in **Visual Studio Code**.

Suggested filename:

```text
highest-score.js
```

Start with:

```js
const scores = [85, 70, 92, 78];
```

Then implement your solution.

Your program should:

```text
Receive the scores
       ↓
Process the scores
       ↓
Find the highest score
       ↓
Display the result
```

Example output:

```text
Highest score: 92
```

---

## Task 6 — Test Your Solution

Test your program with different inputs.

### Test 1

```js
const scores = [85, 70, 92, 78];
```

Expected:

```text
92
```

### Test 2

```js
const scores = [60, 75, 80, 95];
```

Expected:

```text
95
```

### Test 3

```js
const scores = [100, 80, 70];
```

Expected:

```text
100
```

### Test 4

```js
const scores = [50];
```

Expected:

```text
50
```

Test your program and check whether the actual output matches the expected output.

```text
Input
  ↓
Your Program
  ↓
Actual Output
  │
  ▼
Compare
  │
  ├── Matches → Correct
  │
  └── Different → Debug
```

---

## Submission Requirements

Submit the following:

```text
1. Problem Analysis
2. Input and Output
3. Step-by-Step Solution
4. Pseudocode
5. JavaScript Implementation
6. Test Results
```

Suggested project structure:

```text
assignment-module-1/
│
├── highest-score.js
└── README.md
```

Your `README.md` should contain:

```text
# Problem Analysis

Problem:
...

Input:
...

Output:
...

# Steps

1. ...
2. ...
3. ...

# Pseudocode

...

# Test Results

Test 1:
Expected: ...
Actual: ...

Test 2:
Expected: ...
Actual: ...
```

---

## Success Criteria

You have completed the assignment when you can:

```text
✓ Explain the problem
        ↓
✓ Identify the input
        ↓
✓ Identify the output
        ↓
✓ Break the problem into steps
        ↓
✓ Write simple pseudocode
        ↓
✓ Implement the solution in JavaScript
        ↓
✓ Test the solution
```

### Final Challenge

After your solution works, try changing the input:

```js
const scores = [45, 88, 67, 91, 73, 99, 82];
```

Run your program again.

Ask yourself:

> **Does the same algorithm still work?**

If yes, you have successfully created a reusable solution for this type of problem.

---

## Key Takeaway

> **A good solution starts with understanding the problem before writing the code.**

The complete process is:

```text
Problem
   ↓
Input + Output
   ↓
Steps
   ↓
Pseudocode
   ↓
JavaScript
   ↓
Testing
   ↓
Working Solution
```
