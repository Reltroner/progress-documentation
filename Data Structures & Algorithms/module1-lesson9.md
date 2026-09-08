# Why Algorithm Choice Matters

The same problem can often be solved in different ways.

Different algorithms may produce the same result, but they can require different amounts of **time, steps, or memory**.

```text
              PROBLEM
                 │
        ┌────────┴────────┐
        ▼                 ▼
   Algorithm A       Algorithm B
        │                 │
        ▼                 ▼
      Result             Result
````

Both algorithms may be correct.

The difference is **how they reach the result**.

---

## 1. The Same Problem Can Have Different Solutions

Imagine we need to find a name in a list.

```text id="z7s4pa"
["Alice", "Bob", "Charlie", "David"]
```

One approach is to check each name from the beginning:

```text id="x0g6wc"
Alice    → No
Bob      → No
Charlie  → YES
```

Another approach may use a different strategy when the data has the right structure.

```text id="t3v8jq"
Problem
   │
   ▼
Find "Charlie"
   │
   ├── Approach A
   │      └── Check items one by one
   │
   └── Approach B
          └── Use a faster search strategy
```

The result is the same:

```text
"Charlie" found
```

But the amount of work can be different.

---

## 2. More Data Can Expose the Difference

With a small amount of data, different algorithms may appear equally fast.

```text id="7p3m2x"
10 items
   │
   ├── Algorithm A → Fast
   └── Algorithm B → Fast
```

With much more data:

```text id="9w2k6d"
1,000,000 items
        │
        ├── Algorithm A → Much more work
        │
        └── Algorithm B → Less work
```

The difference becomes more noticeable as the input grows.

```text id="a1r5yc"
More Input
    │
    ▼
More Potential Work
    │
    ▼
Algorithm Choice
    │
    ▼
Different Performance
```

---

## 3. Algorithm Choice Affects Performance

An algorithm determines the steps a program performs.

```text id="8j5q4n"
Algorithm
    │
    ▼
Steps
    │
    ▼
Work Performed
    │
    ▼
Program Performance
```

For example:

```text id="s3f8pk"
Search 10 items
     ↓
Small amount of work

Search 1,000,000 items
     ↓
Potentially much more work
```

A good algorithm can reduce unnecessary work.

---

## 4. Correctness Comes First

An algorithm must first produce the **correct result**.

```text id="4y7q2m"
Algorithm
    │
    ▼
Does it solve the problem?
    │
 ┌──┴──┐
 ▼     ▼
YES    NO
 │      │
 ▼      ▼
Evaluate  Fix
efficiency
```

An algorithm that is very fast but produces the wrong result is not a good solution.

```text
Correctness
     ↓
Efficiency
     ↓
Practicality
```

First make the solution correct.

Then consider how efficiently it works.

---

## 5. Algorithms Can Use Different Resources

Algorithm choice is not only about speed.

An algorithm may also use memory and other computing resources.

```text id="r2k8vs"
            Algorithm
                │
       ┌────────┴────────┐
       ▼                 ▼
     Time              Memory
       │                 │
       ▼                 ▼
How much work?      How much space?
```

For example:

```text
Algorithm A
 ├── Uses more steps
 └── Uses less extra memory

Algorithm B
 ├── Uses fewer steps
 └── Uses more extra memory
```

This is called a **trade-off**.

---

## 6. There Is No Universal "Best" Algorithm

An algorithm that is good for one problem may not be the best for another.

```text id="j7m4bc"
Problem A
   │
   ▼
Algorithm A may be suitable


Problem B
   │
   ▼
Algorithm B may be suitable
```

The choice depends on:

```text id="h6v9sq"
Problem
  │
  ├── Input size
  ├── Data organization
  ├── Required operations
  ├── Correctness requirements
  ├── Time requirements
  └── Memory requirements
```

---

## 7. Think About the Problem First

Do not start by asking:

> "Which algorithm do I know?"

Start by asking:

> **"What problem do I need to solve?"**

Then:

```text id="n8p4td"
Problem
   │
   ▼
Understand the Input
   │
   ▼
Understand the Required Result
   │
   ▼
Consider Possible Algorithms
   │
   ▼
Choose a Suitable Approach
   │
   ▼
Implement
   │
   ▼
Test
```

This is a basic problem-solving workflow.

---

## Key Idea

> **Algorithm choice matters because different algorithms can solve the same problem with different amounts of work and resources.**

Remember:

```text id="q2v6ka"
          PROBLEM
             │
             ▼
      Possible Algorithms
             │
       ┌─────┴─────┐
       ▼           ▼
  Algorithm A  Algorithm B
       │           │
       ▼           ▼
    Work A       Work B
       │           │
       └─────┬─────┘
             ▼
        Compare
             │
             ▼
     Choose a suitable
        solution
```

The goal is not to find the **most complicated** algorithm.

The goal is to find an algorithm that is **correct, appropriate, and efficient enough for the problem**.

