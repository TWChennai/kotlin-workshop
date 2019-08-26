```
data class Shop(val name: String, val customers: List<Customer>)

data class Customer(val name: String, val orders: List<Order>)

data class Order(val products: List<Product>, val isDelivered: Boolean)

data class Product(val name: String, val price: Double)

```

* Implement `getMostExpensiveDeliveredProduct` for a Customer.

* Implement `getNumberOfTimesProductWasOrdered` for a shop.
