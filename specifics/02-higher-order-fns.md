## Higher order functions

**A higher-order function is a function that takes functions as parameters, or returns a function**

```kotlin
fun <T> retry(retryLimit: Int, fn: () -> T): T {
    var retryCount = 0
    while (retryCount < retryLimit) {
        try {
            return fn()
        } catch (e: Exception) {
            retryCount++
        }
    }
    throw RuntimeException("All retries are done..")
}

````


```kotlin
retry(TOTAL_RETRIES) {
    println("I will be printed n times...")
}
````

```kotlin
/*lambda can access its closure, i.e. variable declared in outer scope. sum is not part of 
lambda stackframe hence needs to be copied and passed around.*/

var sum = 0
ints.filter { it > 0 }.forEach {
    sum += it
}
println(sum)
```