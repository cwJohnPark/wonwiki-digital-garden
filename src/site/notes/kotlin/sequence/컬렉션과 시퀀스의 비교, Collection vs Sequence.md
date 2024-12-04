---
{"dg-publish":true,"permalink":"/kotlin/sequence/collection-vs-sequence/"}
---


컬렉션

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val result = numbers
    .map { it * 2 }  // 즉시 실행: [2, 4, 6, 8, 10]
    .filter { it > 5 } // 즉시 실행: [6, 8, 10]
println(result) // [6, 8, 10]
```

시퀀스

```kotlin
val numbers = sequenceOf(1, 2, 3, 4, 5) 
val result = numbers 
   .map { it * 2 } // 지연 실행
   .filter { it > 5 } // 지연 실행
   .toList() // 최종 연산: 이때 모든 연산이 실행 
println(result) // [6, 8, 10]
```

| **특징**          | **컬렉션(Collection)**                  | **시퀀스(Sequence)**      |
| --------------- | ------------------------------------ | ---------------------- |
| **처리 방식**       | 즉시 처리(eager evaluation)              | 지연 처리(lazy evaluation) |
| **중간 연산 실행 시점** | 연산 호출 시 바로 실행                        | 최종 연산 호출 시 실행          |
| **메모리 사용**      | 중간 연산마다 새로운 컬렉션 생성                   | 중간 연산 시 새로운 객체 생성 없음   |
| **데이터 크기**      | 작은 크기의 데이터에 적합                       | 큰 크기의 데이터에 적합          |
| **성능**          | 간단한 연산에서 빠르다                         | 복잡한 체이닝 연산에서 효율적       |
| **최종 연산 필요 여부** | 필요 없음                                | 필요 있음                  |
| **사용 사례**       | 소규모 한정적 데이터 처리<br>중간 결과를 저장하거나 확인할 때 | 대규모 또는 무한 데이터 처리       |

#### 컬렉션이 적합한 경우

- 데이터 크기가 작고, 연산이 간단할 때
- 중간 결과를 저장하거나 확인해야 할 때
```kotlin
val smallData = listOf(1, 2, 3)
val transformed = smallData.map { it * 2 }.filter { it > 3 }
println(transformed) // [4, 6]
```

#### 시퀀스가 적합한 경우

- 데이터 크기가 매우 크거나, 무한 스트림을 다룰 때
- 중간 연산을 효율적으로 처리해야 할 때

```kotlin
val largeData = generateSequence(1) { it + 1 } // 무한 시퀀스
val result = largeData
    .map { it * 2 }
    .filter { it % 3 == 0 }
    .take(5) // 무한 시퀀스에서 5개만 가져옴
    .toList()
println(result) // [6, 12, 18, 24, 30]
```