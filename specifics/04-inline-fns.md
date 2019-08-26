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

The inline function `myInlinedFun()` will be expanded at the call site during compile time inside `foo()`. Now foo() will finally look something like

```kotlin
fun foo() {
  println("before")
  print("blaah")
  println("after")
}
```

**Things to note**

* We will lose access to any private variable or function of the class inside the inline function. So it’s better to make functions inline which are very generic and don’t use a class level variable or function to achieve their functionality.

* Do not inline for bigger functions as it degrades the performance.
