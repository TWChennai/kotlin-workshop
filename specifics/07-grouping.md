## Grouping

The Kotlin standard library provides extension functions for grouping collection elements. The basic function groupBy() takes a lambda function and returns a Map.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6)
println(numbers.groupBy { if (it % 2 == 0) "odd" else "even" })
println(numbers.groupBy(keySelector = { if (it % 2 == 0) "odd" else "even"  }, valueTransform = { it * it }))
```
If you want to group elements and then apply an operation to all groups at one time, use the function `groupingBy()`.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6)
println(numbers.groupingBy { if (it % 2 == 0) "odd" else "even" }.fold(0) {acc, element -> acc + element})

```

### Exercise

```
enum class ProductType {
  FRUIT,
  VEGETABLE
}

data class Product(val name: String, val type: ProductType, val quantity: Int) {}

fun data(): List<Product> {
  return listOf(
      Product("Apple", ProductType.FRUIT, 2),
      Product("Potato", ProductType.VEGETABLE, 8),
      Product("Banana", ProductType.VEGETABLE, 13),
      Product("Carrot", ProductType.VEGETABLE, 3),
      Product("Okra", ProductType.VEGETABLE, 4),
      Product("Mango", ProductType.FRUIT, 3)
  )
}

fun getQuantityOf(productType: ProductType): Int {
  // TODO: Implement  
  return 0
}


fun main(){
	data()
    println(getQuantityOf(ProductType.FRUIT))
}

```