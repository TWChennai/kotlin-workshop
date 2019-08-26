```kotlin

//Program entry point
fun main() {
    println("Hello world!")
}

//---Variables---
//vals and vars

val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred

var x = 5 // `Int` type is inferred
x += 1 //changed after assignment

val oneMillion = 1_000_000//underscores for readability

//---Nullability---
val x: Int // Error - variable must be initialized

val x: Int = null // Error - null cannot be a value for non-null type Int
val x: Int? = null // OK
val y: String = null // Error - null cannot be a value for non-null type 
val y: String? = null // OK

//safe call (?)
val name: String? = null
println(name?.length) // prints “null”

//assert (!!) when you know for sure a variable won't be null. if null, causes exception.
var name: String? = null
name = "Treehouse"
println(name!!.length) // prints "9"

department?.head?.name//chaining safe calls

var i: Int? = 10
i?.let { println(it) }//prints i 

i = null
i?.let { println(it) }//no-op

//elvis operator
val l = b?.length ?: -1

fun printName(name: String?) {
    val s = name ?: return //if name is null, returns without printing
    println(s)
}

//---Types----
//Basic types used in Kotlin: numbers, characters, booleans, arrays, and strings.

//---Functions---

//Function without a return type
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}") //string interpolation
}

//Function having two Int parameters with Int return type:
fun sum(a: Int, b: Int): Int {
    return a + b //no semi-colons
}

//Function with an expression body and inferred return type:
fun sum(a: Int, b: Int) = a + b

//example
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return
    }
}

//example
fun maxOf(a: Int, b:Int) = if (a > b) a else 

//Function with nullable Int return type. Compiler forces you to deal with it properly at call site.
fun parseInt(str: String): Int? {
    // ...
}

//---Type Checks and Casts/SmartCasts: 'is' and 'as'---
fun getStringLength(obj: Any): Int? { //Any is a placeholder type for any kind of type. Rarely useful without casting :)
    if (obj !is String) return null

    //can someone tell what the compiler is doing smartly here
    return obj.length
}

//can someone tell what the compiler is doing smartly here.
if (x !is String || x.length == 0) return

//"Unsafe" cast operator
val x: String = y as String //if y is null, it causes exception

//"Safe" cast
val x: String? = y as? String

//---Control flow---
//for loop over array
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}

//for loop over array with indices
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}

//while loop
val items = listOf("apple", "banana", "kiwifruit")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}

//when expression
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }

//when expression with smart casts    
when (x) {
    is Int -> print(x + 1) //smart casts
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}

//range
for (x in 1..5) {
    print(x)
}

//range with step
for (x in 1..10 step 2) {
    print(x)
}

//return. By default returns from the nearest enclosing function or anonymous function.
//break. Terminates the nearest enclosing loop.
//continue. Proceeds to the next step of the nearest enclosing loop.

//break with label
fun loopIt() {
	loop@ for (i in 1..100) {
    	for (j in 1..100) {
        	if (j == 5) break@loop
	        println("i:$i - j:$j")
    	}
	}
}

fun foo() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return // non-local return directly to the caller of foo()
        print(it)
    }
    println("this point is unreachable")
}

fun foo() {
    listOf(1, 2, 3, 4, 5).forEach lit@{
        if (it == 3) return@lit // local return to the caller of the lambda, i.e. the forEach loop
        print(it)
    }
    print(" done with explicit label")
}

fun foo() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return@forEach // local return to the caller of the lambda, i.e. the forEach loop
        print(it)
    }
    print(" done with implicit label")
}

//---Collections---
//A collection contains multiple items that can be accessed through subscripting. 
//Kotlin offers three main types of collections: Arrays, Lists, and Maps.

val cardNames: Array = arrayOf("Jack", "Queen", "King")//explicit type
val cardNames = arrayOf("Jack", "Queen", "King")//implicit type

//access element at 0th index
val firstCard = cardNames[0] // firstCard = "Jack"

//replace value at 0th index
cardNames[0] = "Ace"

//list same as array but can't modify items inside a list

//can modify items inside a mutable list
val cards = mutableListOf("Jack", "Queen", "King")

cards.add("Ace") // Jack, Queen, King, Ace
cards.remove("Jack") // Queen, King, Ace
cards.clear() // empty list
cards.addAll("Jack", "Queen", "King", "Ace

//example
val listWithNulls: List<String?> = listOf("Kotlin", null)
for (item in listWithNulls) {
    item?.let { println(it) } // prints Kotlin and ignores null
}

val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()

//maps
val cards = mapOf("Jack" to 11, "Queen" to 12, "King" to 13)
val jackValue = cards["Jack"] // 11

//to modify values in a map, use mutable map
val mutableCards = mutableMapOf("Jack" to 11, "Queen" to 12, "King" to 13)
cards["Ace"] = 1

//convert map to mutableMap
val mCards = cards.toMutableMap()

//looping a map
val cards = mapOf("Jack" to 11, "Queen" to 12, "King" to 13)
for ((name, value) in cards) {
    println("$name, $value")
}

//use underscore for unused parameter
cards.forEach { _, value -> println("$value!") }

//when
when (cardInt) {
    11 -> println("Jack")
    12 -> println("Queen")
    13 -> println("King")
}

//if returning a value from when expression, it needs to be exhaustive, see the else branch
val cardName = when (cardInt) {
    11 -> "Jack"
    12 -> "Queen"
    13 -> "King"
    else -> "Other"
}

//---Lambdas---
// Lambdas are code blocks enclosed in curly braces.

val items = listOf(1, 2, 3, 4, 5)

items.fold(0, { 
    // When a lambda has parameters, they go first, followed by '->'
    acc: Int, i: Int -> 
    val result = acc + i
    // The last expression in a lambda is considered the return value:
    result
})

// Parameter types in a lambda are optional if they can be inferred:
val joinedToString = items.fold(0, { acc, i -> acc + i })

val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
  .filter { it.startsWith("a") } //it stands for implicit name of a single parameter lambda
  .map { it.toUpperCase() }
  .forEach { println(it) }

//function types
val onClick: () -> Unit = {println("a")}
val onClick: (String) -> Unit = {str -> println(str)}
onClick("AAAA")

//typealias
typealias ClickHandler = (Button, ClickEvent) -> Unit //Unit refers to void/nothing

//a lambda expression
{ a, b -> a + b }

//anonymous function
fun(s: String): Int { return s.toIntOrNull() ?: 0 }

//lambda can access its closure, i.e. variable declared in outer scope
var sum = 0
ints.filter { it > 0 }.forEach {
    sum += it
}
println(sum)

//---Higher Order Functions---
//A higher-order function is a function that takes functions as parameters, or returns a function.

val ints = listOf(1, 2, 3, 4)
ints.filter { it % 2 == 0 }.forEach { value ->
    println(value)
}

```
