---
{"dg-publish":true,"permalink":"/kotlin/sequence/while-sequence-over-while/"}
---

정수 n부터 n을 1씩 늘려가며 가장 가까운 소수를 찾는 함수를 만들어보자.

**while로 구현하기**

```kotlin
fun nextPrimeWhile(n: Int): Int {  
    var i = n + 1  
    while (true) {  
        if (i.isPrime()) {  
            return i  
        }  
        i++  
    }  
}
```


**무한 시퀀스로 구현하기**

```kotlin
fun nextPrime(n: Int): Int =  
    generateSequence(n + 1) { it + 1 }  
        .first { it.isPrime() }
```

무한 시퀀스를 이용하여 N 번째 소수를 찾을 수 있다.

```kotlin
fun nthPrime(n: Int): Int =  
    generateSequence(2) { it + 1 } // 2부터 시작하는 무한 시퀀스  
        .filter { it.isPrime() } // 소수만 필터링  
        .drop(n - 1) // n-1 개의 요소를 건너뛴다  
        .first() // 첫 번째 요소를 반환
        
val prime = nthPrime(10_000)  
println(prime) // 104729
```

- drop 함수는 앞에서부터 n 만큼의 정수를 잘라내어 시퀀스를 리턴한다.
  예를 들어, `[1, 2, 3, 4, 5]` 에 대한 `drop(2)` 는 `[3, 4, 5]` 다.
