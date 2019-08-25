## Data Classes

Data classes are classes whose primary purpose is to hold data (dumb POJOs). The benefit is that the compiler automatically generates

* equals()/hashCode() pair;
* toString() of the form "User(name=John, age=42)";
* componentN() functions corresponding to the properties in their order of declaration;
* copy() function


```kotlin 
data class User(val name: String, val age: Int)
```

Data classes have to fulfill the following requirements:

* The primary constructor needs to have at least one parameter;
* All primary constructor parameters need to be marked as val or var;
* Data classes cannot be abstract, open, sealed or inner;

### Properties Declared in the Class Body

 Compiler only uses the properties defined inside the primary constructor for the automatically generated functions. To exclude a property from the generated implementations, declare it inside the class body:

```kotlin 
data class Person(val name: String) {
    var age: Int = 0
}
```

In above example, only `name`  used inside toString(), equals(), hashCode(), and copy() implementations, only one component function component1().  Two Person objects with different ages will be treated as equal.

### Parameterless constructor
```kotlin
data class User(val name: String = "", val age: Int = 0)
```
### Copy()

Generated copy function looks like
```kotlin
fun copy(name: String = this.name, age: Int = this.age) = User(name, age)
```
Which allows us to copy certain properties and change certain properties like below

```kotlin
val jack = User(name = "Jack", age = 1)
val olderJack = jack.copy(age = 2)
```
### Data Classes and Destructuring Declarations
```kotlin
val jane = User("Jane", 35) 
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"
```
