

## Lists 
* contains()
* list[filter] -> sum(neededBeverages[name = "Beer"].amount)
* index starts at 1; -1 is at the end
* some / every x in [] satisfies condition -> some x in [3500,3000], y in [1200,3100] satisfies x > y
* sum, product, mean, median, stddev, mode, min max, count
* all() - (are all booleans true?) 
* any() - are any booleans true?
* sublist(list, start position, length)
* append(list, items)
* insert before(list, position, newItem)
* remove(list, position)
* reverse(list)
* index of(list, element)
* union(lists) - concat and distinct
* distinct values(list)
* duplicate values(list)
* sort(list, precedes: function<(Any, Any) -> boolean>) A custom function that defines the sorting order. It takes two arguments and returns a boolean indicating whether the first argument should precede the second.
* flatten(nested list)
* concatenate(lists) 
* string join(list, delimiter, prefix, suffix)

## Conditionals
* if c1 AND/ OR c2 then o1 else o2
* for element in list return expression
## Contexts
* context put(context: {x:1}, key: "y", value: 2)

Filters:
```json
[
  {
    name: "Jane",
    age: 22
  },
  {
    name: "William",
    age: 16
  }
][age > 18]

```

- get value(list, key)
- get value(list, keys list)
    - list is for nested contexts - "streetName": get value(company, ["offices", "headquarters", "address", "street"])
- get entries(context) - breakdown of keys and values 


## Functions 
Define a function and variables in a context and use it there.

```json
{
  pi: 3.14159,      
  areaOfCircle : function(radius) (pi * radius * radius),
  result: areaOfCircle(3)
}.result
```
## Temporals
```java
date("2024-06-10")
```
```java
time("14:30:00")
```
```java
date and time("2025-01-01T14:30:00")
```
```java
duration("P1DT6H3M")
```
```java
duration("P1Y6M")
```

addition, substraction, multiplication (of durations), division (of durations also duration / duration = number)

Attributes:
```java

date("2025-04-06").year
date("2025-04-06").day
date("2025-04-06").month
date("2025-04-06").weekday

time("08:00:00").hour
time("08:00:00").minute
time("08:00:00").second

time("08:00:00@Europe/Lisbon").timezone

duration("P3DT2H30M").days
duration("P3DT2H30M").hours

```
```java
now() // returns date and time
today() //returns date
```
*   `day of week()`
*   `day of year()`
*   `week of year()`
*   `month of year()`
*   `last day of month()`

## Hints
* Indexing starts at 1
* Dynamic keys in a context can be achieved by using put.
* When writing complex functions. Pack atomic functions in a context and reference the result of the last one.


## Exercise

Copy this Context in the FEEL Playground (https://camunda.github.io/feel-scala/docs/playground/)
```java
{
  "processInstance": {
        "id": "P123456789",
        "startDate": "2023-01-01T09:00:00Z",
        "tasks": [
            {"id": "T2", "name": "Gather Requirements", "duration": 120, "completed": true},
            {"id": "T6", "name": "Deployment", "duration": 90, "completed": false},
            {"id": "T4", "name": "Implement Solution", "duration": 240, "completed": false},
            {"id": "T3", "name": "Design Solution", "duration": 180, "completed": false},
            {"id": "T5", "name": "Testing & QA", "duration": 180, "completed": false},
            {"id": "T1", "name": "Initial Assessment", "duration": 60, "completed": true}      
        ],
        "variables": {
        "budget": 10000,
        "expenses": 4500,
        "stakeholders": [
            {"name": "Alice", "role": "Sponsor"},
            {"name": "Bob", "role": "Product Owner"},
            {"name": "Charlie", "role": "Lead Developer"}
        ]
    }
  }
}
```
And solve the following tasks. Make sure you save your final solution to a text file, so we can review it.

1.  Calculate Total Duration of Completed Tasks

Write a FEEL expression to calculate the **total duration of all completed tasks**. Update the `processInstance` object by adding a new element `totalCompletedDuration` with the calculated value.

2. Check Budget Status

Write a FEEL expression that compares the current `expenses` against the budget and determines the budget status as "**Under Budget**", "**On Budget**", or "**Over Budget**". Update the processInstance `variables` with a **new key-value** pair `budgetStatus`.

 3. Identify and Sort the Next Task to Complete

Write a FEEL expression to find the **first uncompleted task in the process sorted by `id` in alphabetical order**. Update the processInstance object by adding a new element `nextTask` which should be the `name` of the **next task to complete**.

4. Custom Function for Stakeholder Roles

Create a custom FEEL function named `stakeholderRoles` that takes the stakeholders list and **returns a list of roles**. Use this function to update the processInstance object by adding a new property `rolesList` that contains the list of roles from the stakeholders.



## Other Exercises (Homework)
https://camunda.github.io/feel-scala/docs/playground/?expression-type=expression&expression=Ly8gQ3JlYXRlIGFuIGV4cHJlc3Npb24gdGhhdCBjYWxjdWxhdGVzIHlvdXIgYXNzZXRzIGZvciB3aGVuIHlvdSBhcmUgNjUgeWVhcnMgb2xkIHdpdGhvdXQgaW50ZXJlc3QgY2hhcmdlcw%3D%3D&context=ewogICJhZ2UiOiAyNSwKICAiY3VycmVudEFzc2V0cyI6IDQwMDAsCiAgIm1vbnRobHlSYXRlIjogMzAwCn0%3D - calculate assets with age progression

https://academy.camunda.com/feel-contexts/1981598 - context with filters

