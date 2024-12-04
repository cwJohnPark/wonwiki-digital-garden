---
{"dg-publish":true,"permalink":"/programming/algorithm/fixed-capacity-stack/"}
---


**인스턴스 변수**
- `a[]` 스택의 항목들을 저장하는 배열
- `N` 스택에 들어있는 항목들의 개수를 저장하는 정수

**메서드**
- pop(항목 제거): N 값을 감소하고 새로운 a\[N\] 값을 반환한다.
- push(항목 삽입): a\[N\] 에 새로운 항목을 저장하고 N 값을 증가한다.

규칙
1. 배열에 저장된 항목들은 삽입된 순서를 유지한다.
2. `N` 이 0이면 스택은 비어 있다.
3. 스택의 최상위 항목은 a\[N-1\] 에 위치한다.

다음은 위 규칙을 구현하여 디버그한 예제다.

| StdIn (push/pop) | StdOut | N   | a[0] | a[1] | a[2] | a[3] | a[4] |
| ---------------- | ------ | --- | ---- | ---- | ---- | ---- | ---- |
| to               |        | 1   | to   |      |      |      |      |
| be               |        | 2   | to   | be   |      |      |      |
| or               |        | 3   | to   | be   | or   |      |      |
| not              |        | 4   | to   | be   | or   | not  |      |
| to               |        | 5   | to   | be   | or   | not  | to   |
| -                | to     | 4   | to   | be   | or   | not  |      |
| be               |        | 5   | to   | be   | or   | not  | be   |
| -                | be     | 4   | to   | be   | or   | not  |      |
| -                | not    | 3   | to   | be   | or   |      |      |
| that             |        | 4   | to   | be   | or   | that |      |
| -                | that   | 3   | to   | be   | or   |      |      |
| or               |        | 4   | to   | be   | or   | or   |      |
| -                | or     | 3   | to   | be   | or   |      |      |
| be               |        | 4   | to   | be   | or   | be   |      |
| is               |        | 5   | to   | be   | or   | be   | is   |
| -                | is     | 4   | to   | be   | or   | be   |      |

다음은 고정 용량 스택을 구현한 코드다.

```kotlin
  
class FixedCapacityStack<T>(  
    cap: Int,  
) {  
    private val a: Array<Any?> = arrayOfNulls(cap) // 스택 항목을 저장하는 배열  
    private var n: Int = 0 // 스택 크기  
  
    fun isEmpty(): Boolean = n == 0  
  
    fun size(): Int = n  
  
    fun push(item: T) {  
        if (n == a.size) throw IllegalStateException("Stack overflow") // 용량 초과 시 예외 처리  
        a[n++] = item  
    }  
  
    @Suppress("UNCHECKED_CAST")  
    fun pop(): T {  
        if (isEmpty()) throw NoSuchElementException("Stack is empty")  
        val item = a[--n] as T  
        a[n] = null // 메모리 누수 방지  
        return item  
    }  
}
```

- 클래스 정의에 `<T>`를 추가하여 제너릭 타입을 지원함
- `Array<Any?>`를 사용하여 초기화. Kotlin에서는 제너릭 배열을 직접 생성할 수 없기 때문에 `Any?` 배열로 초기화하고 타입 캐스팅 사용함
- `pop()` 메서드에서 반환 시 `@Suppress("UNCHECKED_CAST")` 어노테이션을 사용하여 경고를 방지함
- `pop()` 호출 후 제거된 요소의 위치를 `null`로 설정하여 메모리 누수 방지함


위 스택에 대한 테스트 코드를 써보자.

```kotlin
@Test  
fun testStack() {  
    val s = FixedCapacityStack<String>(100)  
    val items = arrayOf("to", "be", "or", "not", "to", "-", "be", "-", "-", "that", "-", "-", "-", "is")  
    for (item in items) {  
        if (item == "-") {  
            print("${s.pop()} ") // to be not that or be 
        } else {  
            s.push(item)  
        }  
    }  
    println()  
}
```
