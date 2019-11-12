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
 ```kotlin
 val numbers = listOf(1, 2, 3, 4)
 numbers.filter { it > 2 }.let { println(it.size) }
 ```

It is used in the following cases:
 - Executing a code block only with non-null values. For eg:
   ```kotlin
   val nullableString: String? = "Not null"
   nullableString?.let { println(it.length) }
   ```
 - Introducing local variables with a limited scope for improving code readability. For eg:
   ```kotlin
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
The scope function `also` can be used to side effect in a call chain without breaking it.
It can be simply read as "and also do the following".
- For eg:
  ```kotlin
  api.get()
     .also{Log.debug(it)}
     .map{*/ someother stuff /*}
     ```

### run
It can be used when the lambda contains both the object initialization and the computation of the return value.
-For eg:
  ```kotlin
  val result = service.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}
  ```

### with
The function `with` can be used to logically group calls on an object.
It can be read as "with this object, do the following".
- For eg:
  ```kotlin
  with(message) {
    init("www.message-url.com")
    login(token)
    post("Hi there")
  }
  ```

### apply
The scope function `let` can be used to initialize or configure an object.
It can be simply read as "apply the following assignments to the object".

It is used in the following case:
- To initialize an object. For eg:
  ```kotlin
  val danial = Employee().apply{
    name = "Daniel"
    age = 25
    gender = "male"
  }
  ```

### Mutation of Objects
The following example illustrates how objects are mutated from within scope functions:
```kotlin
fun main() {
    val person: Person? = Person("John", 30)

    val mutationLet = person?.let {
        ++it.age
    }

    println("\nMutation (let): $mutationLet\n")

    val mutationAlso = person?.also {
        ++it.age
    }

    println("\nMutation (also): $mutationAlso\n")

    val mutationRun = person?.run {
        ++age
    }

    println("\nMutation (run): $mutationRun\n")

    val mutationApply = person?.apply {
        ++age
    }

    println("\nMutation (apply): $mutationApply\n")

    person?.let { Person(it.name, ++it.age) }
        ?.let { println("Name: ${it.name}\nAge: ${it.age}\n") }

    println(person)
}

data class Person(var name: String, var age: Long)
```

### Exercises
