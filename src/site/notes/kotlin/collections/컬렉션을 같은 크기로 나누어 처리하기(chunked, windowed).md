---
{"dg-publish":true,"permalink":"/kotlin/collections/chunked-windowed/"}
---


chunked
- 컬렉션을 같은 크기로 나누어 준다.

windowed
- chunked와 동일하게 컬렉션을 같은 크기로 묶어주면서 묶어주는 시작점(step)을 지정할 수 있다.
- 묶어주는 시작점은 기본값이 1이다. 1씩 step을 늘려가며 정해진 chunk 크기만큼 묶어준다.


**chunked 예제**
```kotlin
// 0부터 10까지 정수 리스트  
val list = (0..10).toList()  
// 3개씩 묶어서 출력  
val chunked = list.chunked(3)  
// [[0, 1, 2], [3, 4, 5], [6, 7, 8], [9, 10]]  
assertEquals(  
    listOf(listOf(0, 1, 2), listOf(3, 4, 5), listOf(6, 7, 8), listOf(9, 10)),  
    chunked,  
)
```

 **windowed 예제**
```kotlin
// 0부터 10까지 정수 리스트  
val list = (0..10).toList()  
// 인덱스를 1만큼 이동하면서 3개씩 묶는다.  
val windowed = list.windowed(3)  
assertEquals(  
    listOf(  
        listOf(0, 1, 2),  
        listOf(1, 2, 3),  
        listOf(2, 3, 4),  
        listOf(3, 4, 5),  
        listOf(4, 5, 6),  
        listOf(5, 6, 7),  
        listOf(6, 7, 8),  
        listOf(7, 8, 9),  
        listOf(8, 9, 10),  
    ),  
    windowed,  
)
```

windowed 함수 활용의 가장 보편적인 예시가 이동평균 계산이다.
```kotlin
// 크기가 3인 이동평균 계산  
val movingAverage = list.windowed(3) { it.average() }  
// [1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0]  
assertEquals(  
    listOf(1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0),  
    movingAverage,  
)
```