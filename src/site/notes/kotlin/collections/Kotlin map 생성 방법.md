---
{"dg-publish":true,"permalink":"/kotlin/collections/kotlin-map/"}
---

**1. mapOf() 함수 사용**
가장 기본적인 방법으로, mapOf() 함수를 사용하여 불변(immutable) Map을 생성할 수 있다.

```kotlin
val map1 = mapOf("key1" to 1, "key2" to 2, "key3" to 3)
```

주의할점은 mapOf로 생성된 map은 읽기 전용(불변) 이므로 이후 변경할 수 없다.

**2. mutableMapOf() 함수 사용**
mutableMapOf() 함수를 사용하여 가변(mutable) Map을 생성할 수 있다.

```kotlin
val map2 = mutableMapOf("key1" to 1, "key2" to 2) map2["key3"] = 3 // 새로운 키-값 쌍 추가
```

**3. HashMap 클래스 사용**
Java의 HashMap 클래스를 사용하여 Map을 생성할 수 있다.

```kotlin
val map3 = HashMap<String, Int>() map3["key1"] = 1 map3["key2"] = 2
```

HashMap은 가변 Map으로, 키-값 쌍을 자유롭게 추가, 수정할 수 있다.
Java에서 사용되던 방법이다. map 생성 방법이 명료하진 않다.
Kotlin의 mapOf 함수에 비해 이 방법은 잘 사용하지 않는다.

**4. mapOf와 Pair 사용**
Pair를 사용하여 mapOf 함수로 Map을 생성할 수 있다.

```kotlin
val map4 = mapOf(Pair("key1", 1), Pair("key2", 2), Pair("key3", 3))
```

이 방법은 키와 값을 Pair로 전달하여 Map을 만들 수 있다.
Pair 는 다음과 같이 to 연산자로 대체할 수 있다.

```kotlin
val map = mapOf( Pair(1, "one"), Pair(2, "two"), Pair(3, "three"), ) val map2 = mapOf( 1 to "one", 2 to "two", 3 to "three", )
```

**5. 빈 Map 생성하기**
아무런 요소가 없는 빈 Map을 생성할 수 있다.

불변 빈 Map
```kotlin
val emptyMap1 = emptyMap<String, Int>()
```

가변 빈 Map
```kotlin
val emptyMap2 = mutableMapOf<String, Int>()
```

**6. toMap() 확장 함수 사용**
리스트나 배열을 Map으로 변환하는 toMap() 확장 함수를 사용한다.
```kotlin
val list = listOf("key1" to 1, "key2" to 2, "key3" to 3) val map5 = list.toMap()
```

**7. 빌더 스타일로 buildMap 사용**
Kotlin 1.4부터 추가된 buildMap 함수를 사용하여 Map을 생성할 수 있다.
```kotlin
val map6 = buildMap { put("key1", 1) put("key2", 2) put("key3", 3) }
```

buildMap은 조건에 따른 값 추가, 동적 요소, 복잡한 초기화가 필요한 불변 Map을 만들 때 유용하다.
예를 들어, 다음과 같은 특정 조건에 따라 맵에 요소를 넣을 수 있다.
val map = buildMap { put("key1", 1) if (someCondition) { put("key2", 2) } }

**8. associate 함수**
associate 함수를 사용하여 컬렉션의 각 요소를 특정 키와 값으로 매핑하여 Map을 생성할 수 있다.
각 요소에 대해 람다 함수를 사용해 Pair를 반환하는 방식이다.
```kotlin
val list = listOf("apple", "banana", "cherry") val map = list.associate { fruit -> fruit to fruit.length } println(map) // {apple=5, banana=6, cherry=6}
```

associateWith 함수를 사용하면 to 연산자 함수를 생략하여 더 간단하게 사용할 수 있다.
```kotlin
val list = listOf("apple", "banana", "cherry") 
val map = list.associateWith { fruit -> fruit.length } println(map) // {apple=5, banana=6, cherry=6}
```

associateBy는 key를 받아서 map을 생성해준다. 이 때, value는 list 원래 요소가 매핑된다.

value를 정의해줘야하는 associateWith와는 반대로 생각하면 된다.
```kotlin
val list = listOf("apple", "banana", "cherry") val map = list.associateBy { fruit -> fruit.first() } println(map) // {a=apple, b=banana, c=cherry}
```