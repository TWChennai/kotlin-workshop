## Extension functions

- Kotlin provides the ability to extend a class with new functionality without having to inherit from the class. 
- For example, you can write new functions for a class from a third-party library that you can't modify.
- Such functions are available for calling in the usual way as if they were methods of the original class. 
- This mechanism is called extension functions.
- There are also extension properties that let you define new properties for existing classes.


````
//define extension function
fun MutableList<Int>.swap(index1: Int, index2: Int) {
val tmp = this[index1] // 'this' corresponds to the list
this[index1] = this[index2]
this[index2] = tmp
}

//call extension function
val list = mutableListOf(1, 2, 3)
list.swap(0, 2) // 'this' inside 'swap()' will hold the value of 'list'

//generic example
fun <T> MutableList<T>.swap(index1: Int, index2: Int) {
val tmp = this[index1] // 'this' corresponds to the list
this[index1] = this[index2]
this[index2] = tmp
}
````

