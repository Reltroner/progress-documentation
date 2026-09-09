# Breaking a Problem into Steps

A programming problem can look difficult when we see it as **one big task**.

A useful approach is to break the problem into **smaller, simple steps**.

```text
Big Problem
     │
     ▼
Small Step 1
     │
     ▼
Small Step 2
     │
     ▼
Small Step 3
     │
     ▼
Small Step 4
     │
     ▼
Solution
```

---

## Lesson Objectives

By the end of this lesson, you should be able to:

* **Break** a programming problem into smaller steps.
* **Identify** the actions needed to solve a problem.
* **Arrange** steps in the correct order.
* **Describe** a solution before writing code.
* **Turn** a problem into a simple step-by-step process.

---

## 1. Why Break a Problem Into Steps?

Consider this problem:

> **Find the highest score from a list.**

```text
[85, 70, 92, 78]
        │
        ▼
   Find highest
        │
        ▼
       92
```

Instead of thinking:

```text
"How do I find the highest score?"
```

Break it into smaller questions:

```text
What is the first score?
        ↓
What is the current highest?
        ↓
What is the next score?
        ↓
Is it higher?
        ↓
Should we update the highest?
        ↓
Are there more scores?
```

This makes the problem easier to understand.

---

## 2. Start With a Simple Problem

Example:

```text
Problem:
Find the highest score.
```

Input:

```js
const scores = [85, 70, 92, 78];
```

Expected output:

```text
92
```

Now break the problem down:

```text
Problem
  │
  ▼
Find the highest score
  │
  ├── Start with the first score
  │
  ├── Check the next score
  │
  ├── Compare the scores
  │
  ├── Update the highest if needed
  │
  └── Repeat until finished
```

---

## 3. Step 1 — Start With the First Value

Take the first score:

```text
[85, 70, 92, 78]
 ▲
 │
Start here
```

Set it as the current highest:

```text
highest = 85
```

Visual:

```text
Current highest
      │
      ▼
     85
```

We do not know yet if `85` is the final answer.

It is only our **starting point**.

---

## 4. Step 2 — Check the Next Value

Move to the next score:

```text
[85, 70, 92, 78]
     ▲
     │
   Check
```

Current state:

```text
highest = 85
current = 70
```

Compare:

```text
70 > 85 ?
```

```text
NO
 │
 ▼
Keep highest = 85
```

---

## 5. Step 3 — Compare the Next Value

Move to the next score:

```text
[85, 70, 92, 78]
         ▲
         │
       Check
```

Current state:

```text
highest = 85
current = 92
```

Compare:

```text
92 > 85 ?
```

```text
YES
 │
 ▼
Update highest
 │
 ▼
highest = 92
```

---

## 6. Step 4 — Continue

Move to the last score:

```text
[85, 70, 92, 78]
             ▲
             │
           Check
```

Current state:

```text
highest = 92
current = 78
```

Compare:

```text
78 > 92 ?
```

```text
NO
 │
 ▼
Keep highest = 92
```

There are no more scores.

```text
No more values
      │
      ▼
Return 92
```

---

## 7. The Complete Process

The entire problem can now be represented as:

```text
START
  │
  ▼
[85, 70, 92, 78]
  │
  ▼
Set highest = 85
  │
  ▼
Check 70
  │
  ▼
70 > 85?
  │
  └── NO → Keep 85
              │
              ▼
          Check 92
              │
              ▼
          92 > 85?
           │      │
          YES     NO
           │
           ▼
      Update to 92
           │
           ▼
       Check 78
           │
           ▼
        78 > 92?
           │
           └── NO → Keep 92
                       │
                       ▼
                 No more values
                       │
                       ▼
                    Return 92
```

---

## 8. Turn the Steps Into an Algorithm

After breaking the problem into steps, we can write the algorithm:

```text
1. Take the first score.
2. Set it as the highest score.
3. Get the next score.
4. Compare it with the highest score.
5. If it is higher, update the highest score.
6. Repeat until there are no more scores.
7. Return the highest score.
```

Visualized:

```text
Take first value
      ↓
Set as highest
      ↓
Get next value
      ↓
Compare
      ↓
Higher?
  ┌───┴───┐
 YES      NO
  ↓        ↓
Update    Keep
  │        │
  └───┬────┘
      ↓
More values?
  │       │
 YES      NO
  │        │
  └─→      ↓
        Return
        result
```

---

## 9. Steps Before Code

Breaking a problem into steps helps us separate **thinking** from **coding**.

```text
Problem
   │
   ▼
Break Into Steps
   │
   ▼
Algorithm
   │
   ▼
JavaScript Code
   │
   ▼
Test
```

For example:

```text
Problem
"Find the highest score"
        ↓
Steps
"Compare each score"
        ↓
Algorithm
"Keep the highest value"
        ↓
Code
JavaScript implementation
        ↓
Result
92
```

---

## 10. A Simple Rule

When a problem feels difficult, ask:

```text
"What is the first thing I need to do?"
             │
             ▼
"What comes next?"
             │
             ▼
"What comes after that?"
             │
             ▼
"How do I know when I am finished?"
```

This turns one large problem into a sequence of smaller actions.

```text
Big Problem
     │
     ▼
Small Actions
     │
     ▼
Clear Algorithm
     │
     ▼
Working Solution
```

---

## Key Idea

> **Breaking a problem into smaller steps makes it easier to understand, plan, and solve.**

Remember:

```text
Problem
   ↓
Small Steps
   ↓
Algorithm
   ↓
Code
   ↓
Solution
```

**Think step by step before you write the code.**
