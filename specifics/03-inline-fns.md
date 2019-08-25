## Inline functions

```kotlin
inline fun inlined(block: () -> Unit) {
    println("before")
    block()
    println("after")
}

fun foo() {
    inlined {
    	print("blaah")
    }
}
```
