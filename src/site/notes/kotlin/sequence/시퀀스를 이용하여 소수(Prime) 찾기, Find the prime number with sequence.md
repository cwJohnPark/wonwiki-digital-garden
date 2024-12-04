---
{"dg-publish":true,"permalink":"/kotlin/sequence/prime-find-the-prime-number-with-sequence/"}
---


```kotlin
fun Int.isPrime() =  
    this == 2 ||  
        (2..ceil(sqrt(this.toDouble())).toInt())  
            .none { this % it == 0 }
```

- isPrime 함수를 호출하는 정수가 2인지 확인한다.
- 2가 아니면 2부터 해당 정수의 제곱근 값을 반올림한 수까지를 시퀀스로 생성한다.
- none 함수는 어떠한 시퀀스의 값도 호출한 정수의 값과 나누어 떨어지지 않음을 확인한다.

주어진 정수 다음에 나오는 소수를 찾기
```kotlin
fun Int.nextPrime() =  
    generateSequence(this + 1) { it + 1 }  
        .first { it.isPrime() }
```
- generateSequence 함수의 2개의 인자를 살펴보면, 초기값과 다음의 시퀀스 값을 생성하는 람다함수이다.
- 시퀀스는 first 함수에서 연산을 시작한다.
