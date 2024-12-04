---
{"dg-publish":true,"permalink":"/kotlin/sequence/yield-with-sequence/"}
---


sequence를 생성하는 두 가지 방법
1. 가변인자를 받는 `sequenceOf` 함수
2. 컬렉션에서 시퀀스를 생성하는 `asSequence` 함수
3. 함수 인자를 받는 `geneateSequence` 함수
4. **필요한 갯수만 연산하여 받는 `sequence` 블록**


```kotlin
fun fibonacciSequence() = sequence {  
    var terms = Pair(0, 1)  
    while (true) {  
        yield(terms.first)  
        terms = Pair(terms.second, terms.first + terms.second)  
    }  
}
```

sequence 블록 내부에 무한 while 루프가 있다.
yield 함수가 호출되는 시점에 yield 인자 값인 `terms.first` 를 반환한다.
실제로 무한 while 반복문이지만 무한하게 실행되지 않고 `fibonacciSequence` 시퀀스가 `take` 인자로 주어진 갯수만큼만 연산되어 반환된다.


```kotlin
val fibonacci = fibonacciSequence().take(10).toList()  
println(fibonacci) // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

sequence 블록 함수를 호출하는 클라이언트는 `take` 함수를 사용해 함수 결과 값을 받을 수 있다.


`yieldAll` 함수는 하나의 값만을 반환하는 `yield`와 다르게 여러 값을 반환해준다.

```kotlin
fun fibonacciSequenceWithYieldAll() =  
    sequence {  
        val start = 0  
        yield(start) // 0
        yieldAll(1..5 step 2) // 1, 3, 5  
        yieldAll(generateSequence(8) { it * 3 }) // 8, 24, 72 ...
    }
```
