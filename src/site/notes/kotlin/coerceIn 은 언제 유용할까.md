---
{"dg-publish":true,"permalink":"/kotlin/coerce-in/"}
---

 
Kotlin의 `coerceIn` 함수는 주어진 값이 특정 범위 내로 제한하는 데 사용된다.
이 함수는 값이 범위를 벗어날 경우, 범위의 최소 또는 최대 값 범위 안의 값만 반환해준다.

coerceIn 사용 예시
```kotlin
val value1 = 5 
// 범위: 1과 10을 포함하여 1에서 10 까지 제한한다. 
val coercedValue1 = value1.coerceIn(1, 10) 
// 출력: 5 (범위 내에 있으므로 원래 값 반환) 
println(coercedValue1) 

val value2 = -3 
val coercedValue2 = value2.coerceIn(1, 10) 
// 출력: 1 (값이 최소값보다 작으므로 최소값 반환) 
println(coercedValue2) 

val value3 = 15 
val coercedValue3 = value3.coerceIn(1, 10) 
println(coercedValue3) 
// 출력: 10 (값이 최대값보다 크므로 최대값 반환)
```


`coerceIn` 함수는 값이 특정 범위를 벗어나지 않도록 강제 할 때 유용하다. 
예를 들어, 다음과 같은 경우에서 활용할 수 있습니다:

- **UI 값 제한**: 슬라이더, 스크롤 위치 등 사용자 입력 값이 일정 범위를 넘지 않게 제한하고 싶을 때
```kotlin
val scrollPosition = userInputPosition.coerceIn(0, maxScrollLimit)
```
- **데이터 검증**: 사용자 입력 값이 범위를 초과하지 않도록 제한해야 할 때
```kotlin
val age = inputAge.coerceIn(0, 120) // 나이는 0에서 120 사이로 제한
```
- **게임 개발**: 캐릭터의 체력, 속도 등 값이 0 이하로 떨어지거나 너무 높아지지 않게 관리할 때
```kotlin
val health = playerHealth.coerceIn(0, maxHealth)
```