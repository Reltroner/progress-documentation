# Data in a Program

A program uses data to **perform a task and produce a result**.

The basic flow is:

```text
Input Data
    │
    ▼
┌───────────┐
│  Program  │
└───────────┘
    │
    ▼
Output
````

For example:

```text
User enters age
       │
       ▼
   JavaScript
       │
       ▼
"User is an adult"
```

---

## 1. Data as Program Input

Data can come from different sources.

```text
             DATA
               │
       ┌───────┼────────┐
       ▼       ▼        ▼
     User    File     API
     Input   Data     Data
       │       │        │
       └───────┼────────┘
               ▼
             Program
```

For example:

```js
const name = "Alice";
const age = 25;
```

The values are now available to the program.

```text
name → "Alice"
age  → 25
```

---

## 2. Data Can Be Stored in Variables

A variable gives a program a way to refer to data.

```js
const username = "Alice";
const age = 25;
```

Visualized:

```text
username
   │
   ▼
"Alice"

age
 │
 ▼
25
```

The variable name allows the program to access the stored value.

```js
console.log(username);
console.log(age);
```

Output:

```text
Alice
25
```

---

## 3. Data Can Be Used by the Program

A program can perform operations using stored data.

```js
const price = 100;
const quantity = 3;

const total = price * quantity;
```

The flow is:

```text
price = 100
quantity = 3
     │
     ▼
price × quantity
     │
     ▼
total = 300
```

The program takes existing data and produces new data.

---

## 4. Data Can Change

Some data needs to change while a program is running.

```js
let score = 80;

score = score + 10;
```

Visualized:

```text
Before
  │
  ▼
score = 80
  │
  │ + 10
  ▼
After
  │
  ▼
score = 90
```

This is common in real applications.

For example:

```text
Shopping Cart
     │
     ▼
Add Product
     │
     ▼
Quantity Changes
     │
     ▼
Cart Data Updates
```

---

## 5. Programs Often Work With Many Pieces of Data

A real application rarely works with only one value.

For example, an online store may work with:

```text
Store
│
├── Products
├── Customers
├── Orders
├── Payments
└── Inventory
```

Each part contains data.

```text
Customers
│
├── Alice
├── Bob
└── Charlie

Products
│
├── Laptop
├── Keyboard
└── Mouse
```

The program needs ways to organize and work with all of this information.

---

## 6. Data Flows Through a Program

A simple application can be viewed as a data flow:

```text
        INPUT
          │
          ▼
     ┌──────────┐
     │  STORE   │
     │   DATA   │
     └──────────┘
          │
          ▼
     ┌──────────┐
     │ PROCESS  │
     │   DATA   │
     └──────────┘
          │
          ▼
       OUTPUT
```

For example:

```text
Product Price
      │
      ▼
Quantity
      │
      ▼
Calculate Total
      │
      ▼
Display Total
```

---

## 7. Why This Matters for Data Structures

As the amount of data grows, simply storing values is not enough.

Consider:

```text
10 users
   ↓
100 users
   ↓
10,000 users
   ↓
1,000,000 users
```

The program needs an effective way to organize and access that data.

```text
More Data
    │
    ▼
More Operations
    │
    ▼
Need Better Organization
    │
    ▼
Data Structures
```

This is the connection between **data in a program** and **data structures**.

---

## Key Idea

> **Data in a program is information that the program receives, stores, processes, changes, and uses to produce results.**

The basic pattern is:

```text
INPUT
  │
  ▼
STORE
  │
  ▼
PROCESS
  │
  ▼
OUTPUT
```

As programs handle more complex data, we need better ways to organize it.

That leads to the next concept: **how data is stored in JavaScript.**

