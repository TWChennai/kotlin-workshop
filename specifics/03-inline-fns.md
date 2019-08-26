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


**Things to note**

We will lose access to any private variable or function of the class inside the inline function. So it’s better to make functions inline which are very generic and don’t use a class level variable or function to achieve their functionality.
