## Scope Functions

The Kotlin standard library contains several functions whose sole purpose is to execute a  
block of code within the context of an object.

When one calls any of these scoped functions on an object with an expression, it forms a temporary scope where this object can be accessed with `it` or `this`, without its original name.

There are five scope functions: `let`, `also`, `run`, `with` and `apply`.

### Context Object: it vs this
The functions `run`, `with` and `apply` refer to the context object as a lambda receiver by `this` keyword.

The functions `let` and `also` refer to the context object as a lambda argument, and if not specified the object is accessed by its implicit default name `it`.

### Return Type
The scope functions differ by the result they return:
- `apply` and `also` return the context object.
- `let`, `run`, and `with` return the lambda result.

### Table of Differences
| Function |	Object Reference	| Return Value	| Is Extension Function |
|---|---|---|---|
|let|	it|	Lambda result|	Yes|
|run|	this|	Lambda result|	Yes|
|run|	-|	Lambda result|	No: called without the context object|
|with|	this|	Lambda result|	No: takes the context object as an argument.|
|apply|	this|	Context object|	Yes|
|also|	it|	Context object|	Yes|

### let

The scope function `let` can be used to invoke one or more functions on results of call chains. For eg:
 ```
 val numbers = listOf(1, 2, 3, 4)
 numbers.filter { it > 2 }.let { println(it.size) }
 ```

It is used in the following cases:
 - Executing a code block only with non-null values. For eg:
   ```
   val nullableString: String? = "Not null"
   nullableString?.let { println(it.length) }
   ```
 - Introducing local variables with a limited scope for improving code readability. For eg:
   ```
   val numbers = listOf(1, 2, 3, 4)
   numbers.filter { it > 1 }.let {
       val header = "Header"
       val footer = "Footer"
       val separator = "******"
       println("$header")
       println("$separator")
       it.forEach { println("$it\n$separator") }
       println("$footer")
   }
   ```

### also

### run

### with

### apply

### Exercise