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

The inlined function will be expanded at the call site inside foo() looking something like

```kotlin
fun foo() {
	println("before")
	print("blaah")
	println("after")
}
```