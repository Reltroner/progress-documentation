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
Identify Input & Output
   │
   ▼
Break the Problem Into Steps
   │
   ▼
Write the Algorithm
   │
   ▼
Write the Code
   │
   ▼
Test the Result
```

---

## 1. Start With the Problem

First, identify what needs to be solved.

For example:

> **"Find the highest score from a list of scores."**

```text
Problem
   │
   ▼
Find the highest score
   │
   ▼
Input:
[85, 70, 92, 78]
   │
   ▼
Expected Output:
92
```

Do not start coding immediately.

First, understand what the program needs to accomplish.

---

## 2. Identify the Input

The **input** is the data the program receives.

```text
INPUT
  │
  ▼
[85, 70, 92, 78]
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

The program receives:

```js
const scores = [85, 70, 92, 78];
```

---

## 3. Identify the Expected Output

The **output** is the result the program should produce.

```text
Input
  │
  ▼
[85, 70, 92, 78]
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

The goal is:

```text
Input:
[85, 70, 92, 78]

        ↓

Find the highest value

        ↓

Output:
92
```

Clearly defining the output helps us understand what the algorithm needs to accomplish.

---

## 4. Break the Problem Into Steps

A problem becomes easier to solve when we break it into **small, clear steps**.

Instead of trying to solve everything at once:

```text
"Find the highest score"
```

we can break it down.

### Step 1 — Start With the First Value

Take the first score and temporarily consider it the highest.

```text
Scores:

[85, 70, 92, 78]
  ▲
  │
First score

highest = 85
```

At this point:

```text
Current highest
      │
      ▼
     85
```

We do not know yet whether `85` is actually the highest score.

We only use it as the starting point.

---

### Step 2 — Check the Next Value

Move to the next score:

```text
[85, 70, 92, 78]
      ▲
      │
   Current value

highest = 85
```

Compare:

```text
70 > 85 ?
```

The answer is:

```text
NO
```

So we keep the current highest value:

```text
highest = 85
```

Visualized:

```text
Before:

highest = 85
current = 70

        │
        ▼

70 is NOT higher
        │
        ▼

Keep:

highest = 85
```

---

### Step 3 — Check the Next Value

Move to the next score:

```text
[85, 70, 92, 78]
          ▲
          │
       Current value

highest = 85
```

Compare:

```text
92 > 85 ?
```

The answer is:

```text
YES
```

So we update the highest value:

```text
highest = 92
```

Visualized:

```text
Before:

highest = 85
current = 92

        │
        ▼

92 is higher
        │
        ▼

Update:

highest = 92
```

---

### Step 4 — Check the Last Value

Move to the last score:

```text
[85, 70, 92, 78]
              ▲
              │
           Current value

highest = 92
```

Compare:

```text
78 > 92 ?
```

The answer is:

```text
NO
```

So we keep:

```text
highest = 92
```

Visualized:

```text
Before:

highest = 92
current = 78

        │
        ▼

78 is NOT higher
        │
        ▼

Keep:

highest = 92
```

---

### Step 5 — Finish

There are no more scores.

```text
[85, 70, 92, 78]
                  │
                  ▼
             No more values
                  │
                  ▼
          Return highest
                  │
                  ▼
                  92
```

---

## Step-by-Step Comparison

We can summarize the process in a table.

| Step  | Current Score | Highest Before | Comparison    | Highest After |
| ----- | ------------: | -------------: | ------------- | ------------: |
| Start |             — |              — | —             |            85 |
| 1     |            70 |             85 | 70 > 85 → No  |            85 |
| 2     |            92 |             85 | 92 > 85 → Yes |            92 |
| 3     |            78 |             92 | 78 > 92 → No  |            92 |

The important idea is that `highest` can change during the process.

```text
Start

highest = 85
    │
    ▼
Compare 70
    │
    ▼
Keep 85
    │
    ▼
Compare 92
    │
    ▼
Update to 92
    │
    ▼
Compare 78
    │
    ▼
Keep 92
    │
    ▼
Return 92
```

---

## Complete Process

```text
                 START
                   │
                   ▼
          [85, 70, 92, 78]
                   │
                   ▼
        Take the first value
                   │
                   ▼
           highest = 85
                   │
                   ▼
          Check next value
                   │
                   ▼
             current = 70
                   │
                   ▼
             70 > 85 ?
              │       │
             YES      NO
              │       │
              ▼       ▼
       highest = 70  Keep 85
              │       │
              └───┬───┘
                  ▼
          Check next value
                  │
                  ▼
            current = 92
                  │
                  ▼
            92 > 85 ?
             │       │
            YES      NO
             │       │
             ▼       ▼
      highest = 92  Keep 85
             │       │
             └───┬───┘
                 ▼
         Check next value
                 │
                 ▼
           current = 78
                 │
                 ▼
           78 > 92 ?
            │       │
           YES      NO
            │       │
            ▼       ▼
      highest = 78  Keep 92
            │       │
            └───┬───┘
                ▼
         No more values
                │
                ▼
        Return highest
                │
                ▼
               92
```

The main pattern is:

```text
Take a value
     │
     ▼
Compare it
     │
     ▼
Is it higher?
  │         │
 YES        NO
  │          │
  ▼          ▼
Update     Keep current
highest     highest
  │          │
  └────┬─────┘
       ▼
Check the next value
       │
       ▼
More values?
  │         │
 YES        NO
  │          │
  └──►───────┘
             │
             ▼
        Return result
```

---

## 5. Write the Algorithm Before the Code

Now describe the solution without using JavaScript syntax.

```text
Algorithm:

1. Take the first score as the current highest.
2. Look at the next score.
3. Compare it with the current highest.
4. If it is higher, update the highest.
5. Move to the next score.
6. Repeat until there are no more scores.
7. Return the highest score.
```

For our example:

```text
[85, 70, 92, 78]

highest = 85

70 > 85?
No → keep 85

92 > 85?
Yes → update to 92

78 > 92?
No → keep 92

Result = 92
```

The algorithm describes the **logic** before we worry about programming syntax.

---

## 6. Implement the Solution

Now translate the algorithm into JavaScript.

```js
const scores = [85, 70, 92, 78];

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

The relationship is:

```text
Problem
   │
   ▼
Find highest score
   │
   ▼
Break into steps
   │
   ▼
Algorithm
   │
   ▼
JavaScript Code
   │
   ▼
92
```

---

## 7. Test the Solution

A solution should be tested with different inputs.

### Example 1 — Normal Input

```text
[85, 70, 92, 78]
        │
        ▼
       92
```

### Example 2 — Highest Value Comes First

```text
[100, 80, 70]
    │
    ▼
   100
```

### Example 3 — Highest Value Comes Last

```text
[60, 70, 80, 95]
             │
             ▼
            95
```

### Example 4 — Only One Value

```text
[50]
 │
 ▼
50
```

Testing helps us check whether the solution works correctly.

---

## 8. The Basic Problem-Solving Cycle

A simple programming workflow looks like this:

```text
       ┌────────────────────────┐
       │  1. Understand Problem │
       └────────────┬───────────┘
                    ▼
       ┌────────────────────────┐
       │  2. Identify Input     │
       │     & Output           │
       └────────────┬───────────┘
                    ▼
       ┌────────────────────────┐
       │  3. Break Into Steps   │
       └────────────┬───────────┘
                    ▼
       ┌────────────────────────┐
       │  4. Write Algorithm    │
       └────────────┬───────────┘
                    ▼
       ┌────────────────────────┐
       │  5. Write JavaScript   │
       └────────────┬───────────┘
                    ▼
       ┌────────────────────────┐
       │  6. Test the Solution  │
       └────────────┬───────────┘
                    │
              ┌─────┴─────┐
              │           │
           Correct?       No
              │           │
             YES          ▼
              │       Improve
              ▼           │
            DONE ◄────────┘
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
Small Steps
   ↓
Algorithm
   ↓
JavaScript
   ↓
Test
   ↓
Result
```

For the example:

```text
[85, 70, 92, 78]
        ↓
Compare each score
        ↓
Keep the highest value
        ↓
92
```

The code is only one part of the solution.

**Understanding the problem and designing the steps come first.**
