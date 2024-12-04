---
{"dg-publish":true,"permalink":"/kotlin/scope/let/"}
---


The `let` function in Kotlin is one of the scope functions, allowing an object to be passed into the function body for operations, returning the result. It is mainly used for transforming objects, handling null safety, and making code more readable.


## The signiture of `let`

```kotlin
inline fun <T, R> T.let(block: (T) -> R): R
```

- **T**: The type of the object on which `let` is called.
- **block: (T) -> R**: A lambda function that takes the object as input and performs an operation.
- **R**: The type of the result returned by the lambda function.

## Translated Sentence

- **Object transformation or task execution**: Useful for transforming objects or temporarily using them within the let block.

```kotlin
val number = 5
val result = number.let { it * 2 } // 5를 2배로 변환
println("Transformed result: $result") // 출력: Transformed result: 10
```
  
- **Null safety handling**: Combines let with the safe call operator (?.) to improve code readability.

```kotlin
val nullableString: String? = "Hello, Kotlin!" 

nullableString?.let { 
	// String length: 13 
	println("String length: ${it.length}") 
} 

val nullValue: String? = null 
nullValue?.let { 
	println("It won't be printed") 
}
```

- **Creating a local scope**: Restricts object usage to within a scope, helping to organize code.

```kotlin
val name = "Alice" 
name.let { 
	val greeting = "Hello, $it!" 
	println(greeting) // Hello, Alice! 
} 

// println(greeting) 
// Unresolved reference
```