---
{"dg-publish":true,"permalink":"/kotlin/scope/also/"}
---


also 함수는 부수효과(side effect)를 만들수 있는 스코프 함수다.

```kotlin
public inline fun <T> T.also(block: (T) -> Unit): T
```

- `also`는 원래 객체를 반환하면서 추가 작업을 처리하는 데 적합하다.
- 로깅과 같이 관심사가 다른 작업이 필요한 코드에서 활용도를 높일 수 있다.

#### 파라미터 설명

- `T`: `also`를 호출한 객체의 타입.
- `block: (T) -> Unit`: 객체를 입력받아 수행할 작업.

#### 반환값

- 원래 객체를 반환합니다.

### 예제 코드

#### 1. 로깅 및 디버깅

```kotlin
val person =  
    Person("Alice")  
        .also {  
            println("Person 객체 생성 완료: $it")  
        }  
```

#### 2. 유효성 검사

```kotlin
val person =  
	Person("Alice")  
		.also {  
			require(it.name.isNotBlank()) { "이름이 비어 있습니다." }  
			require(it.age >= 0) { "나이가 음수입니다." }  
		}
```



---

### `also` vs 다른 스코프 함수 비교

| 함수      | 특징                                   | 반환값     | 주요 사용 사례        |
| ------- | ------------------------------------ | ------- | --------------- |
| `also`  | 객체를 그대로 반환. 부수 작업에 사용                | 호출 객체   | 로깅, 디버깅, 체이닝    |
| `apply` | 객체를 반환하지만, 객체의 프로퍼티를 수정 가능 (this 참조) | 호출 객체   | 객체 초기화          |
| `let`   | 람다의 결과를 반환 (it 참조)                   | 람다 결과 값 | 객체 변환           |
| `run`   | 람다의 결과를 반환 (this 참조)                 | 람다 결과 값 | 초기화와 계산이 결합된 경우 |
| `with`  | 객체를 받아 실행하고 람다 결과를 반환                | 람다 결과 값 | 특정 객체에 여러 작업 수행 |