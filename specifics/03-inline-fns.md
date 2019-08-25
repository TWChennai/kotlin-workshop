## Inline functions

**Caution** Using higher-order functions imposes certain runtime penalties: each function is an object, and it captures a closure, i.e. those variables that are accessed in the body of the function. Memory allocations (both for function objects) and virtual calls introduce runtime overhead. 

This is especially important if a higher order function is being invoked within a for loop.

We can avoid the runtime overhead of using higher order functions by inlining the lambda expressions. 

```kotlin
inline fun myInlinedFun(block: () -> Unit) {
    println("before")
    block()
    println("after")
}

fun foo() {
    myInlinedFun {
    	print("blaah")
    }
}
```

The inline function `myInlinedFun()` will be expanded at the call site inside `foo()` looking something like

```kotlin
fun foo() {
	println("before")
	print("blaah")
	println("after")
}
```