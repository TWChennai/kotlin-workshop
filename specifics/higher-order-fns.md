###Higher order functions

**A higher-order function is a function that takes functions as parameters, or returns a function**

````
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


````
retry(TOTAL_RETRIES) {
    println("I will be printed n times...")
}
````

**Caution** Using higher-order functions imposes certain runtime penalties: each function is an object, and it captures a closure, i.e. those variables that are accessed in the body of the function. Memory allocations (both for function objects and classes) and virtual calls introduce runtime overhead.
