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

```kotlin
interface A {
    fun foo() { print("A foo") }
    
    //bar is not marked abstract because that's implicit within
    //an interface declaration if the function has no body.
    fun bar() 
}

interface B {
    fun foo() { print("B foo") }
    fun bar() { print("B bar") }
}

class C : A {
	//we must override bar
    override fun bar() { print("bar") } 
}

//we must override all methods that are common in multiple interfaces and 
//specify exactly how the super implementations should be called
class D : A, B {
    override fun foo() {
        super<A>.foo()
        super<B>.foo()
    }

    override fun bar() {
        super<B>.bar()
    }
}
```