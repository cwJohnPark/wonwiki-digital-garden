---
{"dg-publish":true,"permalink":"/kotlin/scope/apply/"}
---


클래스 생성자 인자만으로는 불가능한 초기화 작업이 있을 경우 `apply` 를 사용할 수 있다.

`apply` 함수는 `this` 를 인자로 전달 하고 `this`를 그대로 리턴하는 함수다.

```kotlin
inline fun <T> T.apply(block: T.() -> Unit): T
```

`apply` 가 잘 활용되는 곳은 데이터베이스 엔티티를 매핑하는 코드다.
