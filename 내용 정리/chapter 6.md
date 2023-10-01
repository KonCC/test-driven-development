# 6장 - 돌아온 ‘모두를 위한 평등’

- 5장에서 중복으로 통과시킨 테스트 청소하기
- 한 클래스가 다른 클래스를 상속하게 하기 (Dollar가 Franc을 상속하거나 Franc이 Dollar를 상속하거나)
    - 어떤 코드도 구원하지 못함
- 두 클래스의 상위 클래스를 찾아내기 (Money)
    - 시간이 걸리긴 하지만 정상 동작

- equals를 일반화해야 함 → Money가 가지고 있으면 어떨까?
- equals를 상위로 올리기 위해 amount 변수도 같이 올림 → 상속할 수 있게 protected (open)로

```kotlin
open class Money() {
    open val amount: Int = 0
}

class Dollar() : Money() {
    override val amount: Int = 5
}
```

- equals일반화

```kotlin
//Dollar class

fun equals(object: Any): Boolean{
	val money: **Money** = (**Money**) object
	return amount == money.amount
}
```

- 기존 Dollar의 equals부분에서 임시 변수 타입 Money로 변경
- 변수의 이름도 money로 변경 → Money 클래스로 옮길 수 있게 됨

Franc의 equals()

- Franc의 equals 테스트가 없는 상태
- 적절한 테스트가 없는 경우에서 TDD를 해야하는 경우
    - 있으면 좋을 것 같은 테스트를 작성
    - 그렇지 않으면 리팩토링하다가 뭔가 깨트릴 것이다.

- franc의 equals를 dollar 테스트를 복붙한다.

```kotlin
fun testEquality() {
	assertTrue(Dollar(5).equals(Dollar(5))
	assertFalse(Dollar(5).equals(Dollar(6))
	assertTrue(Franc(5).equals(Franc(5))
	assertFalse(Franc(5).equals(Franc(6))
}
```

- Franc도 Dollar랑 똑같이 Money를 상속받아서 amount랑 equals를 Money로 올릴 수 있다.

## 검토

- 공통된 코드를 Dollar(하위)에서 Money(상위)로 올렸다 (amount, equals())
- Franc도 동일하게 공통된 코드를 Money로 올렸다
- 불필요한 구현을 제거하기 전에 두 equals() 구현을 일치시켰다
