## Sealed Classes

Sealed classes are, in a sense, extension of `Enum` classes. 
*  Sealed class is abstract by itself i.e. it cannot be instantiated directly and can have abstract members.
* A sealed class can have subclasses, but all of them must be declared in the same file as the sealed class itself.

```kotlin
enum class BasicScreenState {
    ERROR,
    LOADING,
    DATA
}
```

Let's say we are fetching some data async from the network and we are tracking our UI screen state using the above enum during the fetch.

```kotlin
fun setBasicScreenState(basicScreenState: BasicScreenState) {
    when(basicScreenState) {
        BasicScreenState.ERROR -> { /* set error state in the view */ }
        BasicScreenState.LOADING -> { /* set loading state in the view */ }
        BasicScreenState.DATA -> { /* hide loading or error states in the view */ }
    }
}

fun displayData(someData: SomeData) {
    // actually display the data in the view
    //sometextView.text = someData.name
}
```
We are calling 2 functions to handle our success state setBasicScreenState() and displayData().

What if we wanted to hold someData in the enum itself to handle the success case in the when expression above and avoid call to displayData(). It would look something like this.

```kotlin
enum class ScreenStateField(val someData: SomeData) {
    ERROR(SomeData("1", "some data 1")),
    LOADING(SomeData("2", "some data 2")),
    DATA(SomeData("3", "some data 3"))
}
```
But here we have to create Error, Loading states with dummy SomeData assuming we are fetching it from network.

We can achieve this using Sealed classes and when expressions

```kotlin
sealed class ScreenState {
    data class Error(val errorMessage: String) : ScreenState()
    data class Loading() : ScreenState()
    data class Data(val someData: SomeData) : ScreenState()
}

fun setScreenState(screenState: ScreenState) {
    when(screenState) {
        is ScreenState.Error -> { /* set error state in the view */ }
        is ScreenState.Loading -> { /* set loading state in the view */ }
        is ScreenState.Data -> {
            /* hide loading or error states in the view and display data*/
            //sometextView.text = screenState.someData.name
        }
    }
}
```


