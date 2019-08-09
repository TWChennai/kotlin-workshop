## Inline functions

````
inline fun inlined(block: () -> Unit) {
    println("hi!")
}

fun foo() {
    inlined {
        return // OK: the lambda is inlined
    }
}
````
