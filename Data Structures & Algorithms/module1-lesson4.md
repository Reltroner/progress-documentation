# Working with Multiple Values

Real programs rarely work with only one value.

For example, an online store may need to work with many products:

```text
Products
│
├── Laptop
├── Keyboard
├── Mouse
├── Monitor
└── Headset
````

Instead of creating a separate variable for every product:

```js
const product1 = "Laptop";
const product2 = "Keyboard";
const product3 = "Mouse";
```

we can group the values into a collection:

```js
const products = [
  "Laptop",
  "Keyboard",
  "Mouse"
];
```

Visualized:

```text
products
   │
   ▼
┌──────────┬──────────┬────────┐
│  Laptop  │ Keyboard │ Mouse  │
└──────────┴──────────┴────────┘
     0          1          2
```

---

## 1. Why Work With Multiple Values?

A program may need to process many values as one group.

```text
             Application
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
     Products   Users      Orders
        │         │         │
        ▼         ▼         ▼
     Many data  Many data  Many data
```

For example:

```text
10 products
100 users
1,000 orders
```

The program needs a way to work with these values efficiently.

---

## 2. A Collection Groups Related Values

A collection allows multiple values to be handled together.

```js
const scores = [80, 90, 75, 88];
```

Visualized:

```text
scores
  │
  ▼
┌────┬────┬────┬────┐
│ 80 │ 90 │ 75 │ 88 │
└────┴────┴────┴────┘
  0    1    2    3
```

Instead of thinking about four separate values:

```text
80
90
75
88
```

we can think about one collection:

```text
scores
   │
   └── [80, 90, 75, 88]
```

---

## 3. Accessing Individual Values

When working with an array, each value can be accessed using its **index**.

```js
const scores = [80, 90, 75, 88];

console.log(scores[1]);
```

Visualized:

```text
scores
  │
  ▼
┌────┬────┬────┬────┐
│ 80 │ 90 │ 75 │ 88 │
└────┴────┴────┴────┘
  0   [1]   2    3
       │
       ▼
      90
```

Output:

```text
90
```

Remember:

> **An index identifies the position of an item in an array.**

JavaScript starts array indexes at `0`.

---

## 4. Working With Every Value

Programs often need to process every item in a collection.

For example:

```js
const scores = [80, 90, 75];

for (const score of scores) {
  console.log(score);
}
```

Visualized:

```text
scores
  │
  ▼
┌────┬────┬────┐
│ 80 │ 90 │ 75 │
└────┴────┴────┘
  │    │    │
  ▼    ▼    ▼
Process each value
```

Output:

```text
80
90
75
```

This process is called **iteration**.

> **Iteration = going through the values in a collection one by one.**

---

## 5. Working With Collection Data

Once data is grouped together, a program can perform operations on the collection.

```text
Collection
    │
    ├── Read
    ├── Add
    ├── Remove
    ├── Update
    ├── Search
    └── Process
```

For example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];
```

A program might:

```text
products
   │
   ├── Add a product
   │
   ├── Remove a product
   │
   ├── Find a product
   │
   └── Display products
```

These operations are common in real applications.

---

## 6. Collections Can Contain Objects

Real application data is often more than simple values.

For example, a product can have several properties:

```js
const products = [
  {
    name: "Laptop",
    price: 1000
  },
  {
    name: "Mouse",
    price: 25
  }
];
```

Visualized:

```text
products
   │
   ├── Product 1
   │     ├── name  → "Laptop"
   │     └── price → 1000
   │
   └── Product 2
         ├── name  → "Mouse"
         └── price → 25
```

This is a common pattern:

```text
Array
  │
  ├── Object
  ├── Object
  ├── Object
  └── Object
```

It allows a program to work with a **collection of structured data**.

---

## 7. The Bigger Picture

Working with multiple values introduces an important programming problem:

```text
Many Values
     │
     ▼
How should we organize them?
     │
     ▼
How should we access them?
     │
     ▼
How should we search them?
     │
     ▼
How should we process them?
```

Different data structures provide different ways to solve these problems.

```text
Many Values
     │
     ▼
Data Structure
     │
     ▼
Access + Search + Processing
```

For example:

```text
Array
  │
  └── Ordered collection

Object
  │
  └── Related properties

Later:
Map
  │
  └── Key-based lookup

Stack
  │
  └── Last-in, first-out

Queue
  │
  └── First-in, first-out
```

---

## Key Idea

> **Working with multiple values means treating related data as a collection so a program can access, process, search, and manage the values together.**

The basic progression is:

```text
Multiple Values
      │
      ▼
   Collection
      │
      ▼
Organize the Data
      │
      ▼
Access & Process
      │
      ▼
Choose the Right
Data Structure
```

As the amount and complexity of data increases, choosing the right way to organize it becomes more important.

