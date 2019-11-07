### Interfaces

- Interfaces are a way of defining public contracts. 
- Interfaces are just declarations (generally). 
- Interfaces have to be implemented to get behaviours for the declarations. 
- Classes implement interfaces and provide the concrete behaviours. 

### Kotlin Interfaces
	
- Can contain abstract methods and implementations
- Cannot contain state (properties with backing fields)
- Can contain abstract properties and accessor implementations for these properties but properties cannot have a backing field (state)


```kotlin
//declaration

interface MyInterface {
	fun foo()
	fun bar() {
		println("bar")
	}
}

//implementation

class A: MyInterface {
	override fun foo() {
		println("overridden foo")
	}
}
```

### Interface with Properties

```kotlin
//declaration

interface MyInterfaceWithProps {
	val prop: Int

	val propWithImplementation: String
		get() = "propWithImplementation"

	fun foo() {
		print(prop)
	}
}

//implementation

class B: MyInterfaceWithProps {
	override val prop: Int = 11
}
```

### Interface Inheritance

```kotlin
interface Named {
	val name: String
}


interface Person: Named {
	val firstName: String
	val lastName: String
	override val name: String get() = "$firstName $lastName"
}

data class Employee(
	//implementing name is not required because there is an implementation in Person interface
	override val firstName: String,
	override val lastName: String,
	val position: Position
	): Person
```

### Resolving Interface Conflicts (Multiple Interface Inheritance)

