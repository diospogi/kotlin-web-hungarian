---
type: doc
layout: reference
category: "Collections"
title: "Grouping"
---

# Grouping

The Kotlin standard library provides extension functions for grouping collection elements.
The basic function `groupBy()` takes a lambda function and returns a `Map`.
In this map, each key is the lambda result and the corresponding value is the `List` of elements on which this result is returned.
This function can be used, for example, to group a list of `String`s by their first letter. 

You can also call `groupBy()` with a second lambda argument – a value transformation function.
In the result map of `groupBy()` with two lambdas, the keys produced by `keySelector` function are mapped to the results of the value transformation function instead of the original elements.

<div class="sample" markdown="1" theme="idea" data-min-compiler-version="1.3">

```kotlin
fun main() {
//sampleStart
    val numbers = listOf("one", "two", "three", "four", "five")

    println(numbers.groupBy { it.first().toUpperCase() })
    println(numbers.groupBy(keySelector = { it.first() }, valueTransform = { it.toUpperCase() }))
//sampleEnd
}
```
</div>

If you want to group elements and then apply an operation to all groups at one time, use the function `groupingBy()`.
It returns an instance of the `Grouping` type.
The `Grouping` instance stores all the returned groups together and lets you easily apply operations to them all.

Namely, `Grouping` supports the following operations:

* `eachCount()` counts the elements in each group. 
* `fold()` and `reduce()` perform [fold and reduce](collection-aggregate.html#fold-and-reduce) operations on each group as a separate collection and return the results.
* `aggregate()` applies a given operation subsequently to all the elements in each group and returns the result.
   This is the generic way to perform any operations on a `Grouping`. Use it to implement custom operations when fold or reduce are not enough.

<div class="sample" markdown="1" theme="idea" data-min-compiler-version="1.3">

```kotlin
fun main() {
//sampleStart
    val numbers = listOf("one", "two", "three", "four", "five", "six")
    println(numbers.groupingBy { it.first() }.eachCount())
//sampleEnd
}
```
</div>
