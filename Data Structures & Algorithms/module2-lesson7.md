# Iterating Through an Array

Sometimes a program needs to work with **every value** in an array.

For example, an application may need to:

* Display every product.
* Calculate all scores.
* Check every task.
* Print every user.
* Process every order.

Instead of accessing each index manually:

```js
console.log(products[0]);
console.log(products[1]);
console.log(products[2]);
```

we can **iterate** through the array.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Understand what iteration means.
* Use a `for` loop to iterate through an array.
* Access each array value during iteration.
* Use the array length to control a loop.
* Understand the basic `for...of` loop.

---

## 1. What Does Iterating Mean?

**Iterating** means going through items one by one.

For example:

```text
Array

┌────────┬────────┬──────────┬─────────┐
│ Laptop │ Mouse  │ Keyboard │ Monitor │
└────────┴────────┴──────────┴─────────┘
    │        │          │          │
    ▼        ▼          ▼          ▼
   Step 1   Step 2     Step 3     Step 4
```

The program processes each item in order.

```text
Start
  │
  ▼
Laptop
  │
  ▼
Mouse
  │
  ▼
Keyboard
  │
  ▼
Monitor
  │
  ▼
End
```

This process is called **iteration**.

---

## 2. Iterating with a `for` Loop

One common way to iterate through an array is with a `for` loop.

Example:

```js id="8v4z1s"
const products = ["Laptop", "Mouse", "Keyboard"];

for (let i = 0; i < products.length; i++) {
  console.log(products[i]);
}
```

Output:

```text id="3q9w6k"
Laptop
Mouse
Keyboard
```

The loop accesses each index:

```text id="q3a1x8"
i = 0 → products[0] → Laptop
i = 1 → products[1] → Mouse
i = 2 → products[2] → Keyboard
```

---

## 3. How the `for` Loop Works

Look at the loop:

```js id="y9h4dc"
for (let i = 0; i < products.length; i++) {
  console.log(products[i]);
}
```

It has three important parts:

```text id="t4g2kp"
for (
  let i = 0;       → Start
  i < products.length; → Condition
  i++              → Move to next index
)
```

The process is:

```text id="7s5h3a"
Start i = 0
    │
    ▼
Process products[0]
    │
    ▼
i++
    │
    ▼
Process products[1]
    │
    ▼
i++
    │
    ▼
Process products[2]
    │
    ▼
Stop when condition is false
```

---

## 4. Why Use `products.length`?

The array length tells us how many items exist.

```js id="e1s7cp"
const products = ["Laptop", "Mouse", "Keyboard"];

console.log(products.length);
```

Output:

```text id="w3r8ax"
3
```

So this condition:

```js id="5g8v2m"
i < products.length
```

means:

> Continue while `i` is a valid array index.

The indexes are:

```text id="a2v6kp"
Length = 3

Index:
  0     1     2
  │     │     │
  ▼     ▼     ▼
[Laptop, Mouse, Keyboard]
```

There is no index `3`.

Therefore:

```text id="m5r1zc"
i = 0 → process
i = 1 → process
i = 2 → process
i = 3 → stop
```

---

## 5. Accessing the Current Value

Inside the loop:

```js id="x6z0vn"
products[i]
```

means:

> Get the value at the current index.

Example:

```js id="n8m2qa"
const products = ["Laptop", "Mouse", "Keyboard"];

for (let i = 0; i < products.length; i++) {
  console.log(products[i]);
}
```

Visual:

```text id="1s8v2c"
          i
          │
          ▼
┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘
    0        1          2
    ▲
    │
 products[i]
```

When `i` changes, the accessed value changes.

---

## 6. Processing Every Value

Iteration is not only for displaying data.

You can perform an operation for every item.

For example, calculate the total score:

```js id="z4p8kw"
const scores = [85, 70, 92, 78];

let total = 0;

for (let i = 0; i < scores.length; i++) {
  total += scores[i];
}

console.log(total);
```

Output:

```text id="d8q2hn"
325
```

Visual:

```text id="g7m3rx"
85 → total = 85
70 → total = 155
92 → total = 247
78 → total = 325
```

The loop processes every value one by one.

---

## 7. Iterating with `for...of`

JavaScript also provides a simpler way to iterate through array values:

```js id="k2d7vp"
const products = ["Laptop", "Mouse", "Keyboard"];

for (const product of products) {
  console.log(product);
}
```

Output:

```text id="x6q1bz"
Laptop
Mouse
Keyboard
```

The `for...of` loop gives you the **value directly**.

```text id="n4c7ws"
products
   │
   ▼
┌────────┬────────┬──────────┐
│ Laptop │ Mouse  │ Keyboard │
└────────┴────────┴──────────┘
    │        │          │
    ▼        ▼          ▼
 product   product    product
```

You do not need to manually use an index.

---

## 8. `for` vs `for...of`

Both can iterate through an array.

### Using `for`

```js id="v2r5nk"
for (let i = 0; i < products.length; i++) {
  console.log(products[i]);
}
```

You work with the **index**.

### Using `for...of`

```js id="c7m1qa"
for (const product of products) {
  console.log(product);
}
```

You work directly with the **value**.

Visual:

```text id="r5k9tx"
              Iteration
                  │
          ┌───────┴───────┐
          ▼               ▼
        for           for...of
          │               │
          ▼               ▼
      index + value      value
```

For simple iteration where you only need the values, `for...of` is often easier for beginners.

---

## 9. Iterating Through Objects

Arrays can contain objects.

For example:

```js id="j6p3wf"
const products = [
  { name: "Laptop", price: 1200 },
  { name: "Mouse", price: 25 },
  { name: "Keyboard", price: 50 }
];
```

You can iterate through the products:

```js id="w8s2ld"
for (const product of products) {
  console.log(product.name);
}
```

Output:

```text id="r9x4mc"
Laptop
Mouse
Keyboard
```

You can also access other properties:

```js id="m3v7qa"
for (const product of products) {
  console.log(product.name, product.price);
}
```

Output:

```text id="c5n8zp"
Laptop 1200
Mouse 25
Keyboard 50
```

Visual:

```text id="f4k1ys"
products
   │
   ▼
┌──────────────┐
│ Laptop $1200 │
├──────────────┤
│ Mouse $25    │
├──────────────┤
│ Keyboard $50 │
└──────────────┘
       │
       ▼
   Process each
      product
```

---

## 10. A Real-World Example

Imagine a simple shopping application.

The application needs to display every product:

```js id="b6w3ne"
const products = [
  "Laptop",
  "Mouse",
  "Keyboard",
  "Monitor"
];

for (const product of products) {
  console.log(`Product: ${product}`);
}
```

Output:

```text id="q8m2xr"
Product: Laptop
Product: Mouse
Product: Keyboard
Product: Monitor
```

The same idea can be used for:

* Product lists
* Task lists
* Student scores
* Orders
* Messages
* User records

---

## 11. Iteration and Array Operations

Iteration is an important foundation for many array operations.

For example:

```text id="k7p4mz"
Array
  │
  ▼
Iterate through values
  │
  ├── Check a value
  ├── Calculate something
  ├── Display a value
  ├── Compare values
  └── Transform data
```

Later lessons will use iteration to understand operations such as:

* Finding an item.
* Filtering data.
* Transforming data.

---

## Key Idea

**Iterating through an array means processing its values one by one.**

A traditional `for` loop gives you access to the index:

```js id="q2v7mc"
for (let i = 0; i < products.length; i++) {
  console.log(products[i]);
}
```

A `for...of` loop gives you the value directly:

```js id="a8n3zk"
for (const product of products) {
  console.log(product);
}
```

Remember:

```text id="w6p1yr"
Array
  │
  ▼
Iterate
  │
  ├── Item 1
  ├── Item 2
  ├── Item 3
  └── ...
```

**Iteration allows a program to work with every item in a collection instead of accessing each item manually.**
