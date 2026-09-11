# Updating Array Data

Array data can change after it has been created.

For example, a product price may change, a student's score may be corrected, or a task name may need to be updated.

JavaScript allows us to update a specific array value by using its **index**.

---

## Lesson Objectives

By the end of this lesson, you will be able to:

* Update a value inside an array.
* Use an index to identify the value to change.
* Replace an existing array value.
* Update data stored in variables.
* Understand how indexes change when array data is updated.

---

## 1. Updating a Value Using an Index

To update an array value, use its index and assign a new value.

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products[1] = "Wireless Mouse";

console.log(products);
```

Output:

```text
["Laptop", "Wireless Mouse", "Keyboard"]
```

The value at index `1` was replaced.

Visual:

```text
Before

Index:     0          1           2
           │          │           │
           ▼          ▼           ▼
        ┌──────┬──────────┬──────────┐
        │Laptop│  Mouse   │ Keyboard │
        └──────┴──────────┴──────────┘
                     │
                     │ update
                     ▼
              "Wireless Mouse"

After

        ┌──────┬─────────────────┬──────────┐
        │Laptop│ Wireless Mouse  │ Keyboard │
        └──────┴─────────────────┴──────────┘
```

---

## 2. The Basic Pattern

The basic pattern is:

```js
array[index] = newValue;
```

For example:

```js
const scores = [85, 70, 92, 78];

scores[1] = 75;

console.log(scores);
```

Output:

```text
[85, 75, 92, 78]
```

Only the value at index `1` changed.

```text
Index:    0    1    2    3
          │    │    │    │
          ▼    ▼    ▼    ▼
Before:  [85,  70,  92,  78]
               │
               ▼
              75

After:   [85,  75,  92,  78]
```

---

## 3. Updating the First Value

Remember that the first array value has index `0`.

```js
const students = ["Alice", "Bob", "Charlie"];

students[0] = "Anna";

console.log(students);
```

Output:

```text
["Anna", "Bob", "Charlie"]
```

Visual:

```text
Before:

[Alice] [Bob] [Charlie]
   0      1       2
   │
   ▼
Update index 0


After:

[Anna] [Bob] [Charlie]
```

---

## 4. Updating the Last Value

You can also update the last value.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products[2] = "Mechanical Keyboard";

console.log(products);
```

Output:

```text
["Laptop", "Mouse", "Mechanical Keyboard"]
```

The index stays the same:

```text
Before:

Index:      0        1          2
            │        │          │
            ▼        ▼          ▼
         [Laptop] [Mouse] [Keyboard]

                                  │
                                  ▼
                         Replace value


After:

Index:      0        1                  2
            │        │                  │
            ▼        ▼                  ▼
         [Laptop] [Mouse] [Mechanical Keyboard]
```

Updating a value does **not** automatically change its position.

---

## 5. Updating Data with a Variable

The new value can come from a variable.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

const updatedProduct = "Gaming Mouse";

products[1] = updatedProduct;

console.log(products);
```

Output:

```text
["Laptop", "Gaming Mouse", "Keyboard"]
```

The variable provides the new value:

```text
updatedProduct
      │
      ▼
"Gaming Mouse"
      │
      ▼
products[1]
      │
      ▼
Array value is replaced
```

This becomes useful when the new data comes from user input, a form, an API, or another part of a program.

---

## 6. Updating Numbers

Arrays can contain numbers, so numerical values can also be updated.

```js
const scores = [85, 70, 92, 78];

scores[0] = 90;

console.log(scores);
```

Output:

```text
[90, 70, 92, 78]
```

Visual:

```text
Before:

[85] [70] [92] [78]
  0    1    2    3
  │
  ▼
Change to 90


After:

[90] [70] [92] [78]
```

---

## 7. Updating Objects Inside an Array

Arrays can contain objects.

You can access an object using its index and then update one of its properties.

Example:

```js
const products = [
  { name: "Laptop", price: 1200 },
  { name: "Mouse", price: 25 }
];

products[1].price = 30;

console.log(products);
```

The result is:

```text
[
  { name: "Laptop", price: 1200 },
  { name: "Mouse", price: 30 }
]
```

Visual:

```text
products
   │
   ▼
┌──────────────────────┐
│ 0 → Laptop  $1200    │
│ 1 → Mouse   $25      │
└──────────────────────┘
             │
             │ update price
             ▼
          $30
```

The array position stays the same, but the object's data changes.

---

## 8. Updating an Array Inside a Program

Consider a task management application:

```js
const tasks = [
  "Learn JavaScript",
  "Practice Arrays",
  "Build a Project"
];
```

Suppose the second task is changed.

```js
tasks[1] = "Practice Data Structures";

console.log(tasks);
```

Output:

```text
[
  "Learn JavaScript",
  "Practice Data Structures",
  "Build a Project"
]
```

Visual:

```text
Before:

┌───────────────────────┐
│ Learn JavaScript      │
│ Practice Arrays       │ ← update
│ Build a Project       │
└───────────────────────┘

                 ↓

After:

┌─────────────────────────────┐
│ Learn JavaScript            │
│ Practice Data Structures    │
│ Build a Project             │
└─────────────────────────────┘
```

This pattern is common in applications that allow users to edit existing data.

---

## 9. Updating vs Adding Data

Updating and adding are different operations.

### Updating

An existing value is replaced:

```js
products[1] = "Monitor";
```

```text
Before:
[Laptop, Mouse, Keyboard]

After:
[Laptop, Monitor, Keyboard]
```

The number of items stays the same.

### Adding

A new value is added:

```js
products.push("Monitor");
```

```text
Before:
[Laptop, Mouse, Keyboard]

After:
[Laptop, Mouse, Keyboard, Monitor]
```

The number of items increases.

Visual:

```text
             Array Data
                 │
        ┌────────┴────────┐
        ▼                 ▼
     Update              Add
        │                 │
        ▼                 ▼
 Replace a value      Add a value
 at an index          to the collection
```

---

## 10. Updating vs Removing Data

Removing and updating also have different effects.

```js
const products = ["Laptop", "Mouse", "Keyboard"];
```

Updating:

```js
products[1] = "Monitor";
```

Result:

```text
["Laptop", "Monitor", "Keyboard"]
```

The array still contains **3 items**.

Removing:

```js
products.splice(1, 1);
```

Result:

```text
["Laptop", "Keyboard"]
```

The array now contains **2 items**.

```text
Update:
[Laptop, Mouse, Keyboard]
          ↓
[Laptop, Monitor, Keyboard]

Same number of items


Remove:
[Laptop, Mouse, Keyboard]
          ↓
[Laptop, Keyboard]

Fewer items
```

---

## 11. What Happens to the Index?

When you update a value, its index does not change.

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products[1] = "Monitor";
```

The result is:

```text
Index:    0        1          2
          │        │          │
          ▼        ▼          ▼
       [Laptop] [Monitor] [Keyboard]
```

Index `1` still points to the second item.

This is different from removing data, where later items may move to different indexes.

---

## 12. A Simple Real-World Example

Imagine an online store.

A product's price needs to be updated:

```js
const prices = [1200, 25, 50];

prices[1] = 30;

console.log(prices);
```

Output:

```text
[1200, 30, 50]
```

The program identified the product by its position and replaced its old price.

```text
Before:

Laptop     Mouse     Keyboard
$1200      $25       $50
             │
             ▼
         Update price
             │
             ▼
            $30

After:

Laptop     Mouse     Keyboard
$1200      $30       $50
```

---

## Key Idea

To update an existing value in an array, use its **index** and assign a new value:

```js
array[index] = newValue;
```

Example:

```js
const products = ["Laptop", "Mouse", "Keyboard"];

products[1] = "Monitor";

console.log(products);
```

Result:

```text
["Laptop", "Monitor", "Keyboard"]
```

Remember:

```text
Update → Replace an existing value
Add    → Add a new value
Remove → Delete an existing value
```

**An array index gives your program a direct position to update when existing collection data needs to change.**
