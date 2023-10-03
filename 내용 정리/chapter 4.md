# 4장 프라이버시

```kotlin
fun testMultiplication() {
	val five = Dollar(5)
	var product: Dollar = five.times(2)
	assertEquals(10, product.amount)
	product = five.times(3)
	assertEquals(15, product.amount)
}
```

- 기존의 코드는 테스트가 정확히 원하는 바를 말하지 않는다
    - 객체의 값에 원하는 곱수만큼의 값을 가지는 객체를 반환한다는 원하는바

```kotlin
fun testMultiplication() {
	val five = Dollar(5)
	var product: Dollar = five.times(2)
	assertEquals(Dollar(10), product.amount)
	product = five.times(3)
	assertEquals(Dollar(15), product.amount)
}
```

- 비교 대상을 객체로 변경해줌
- 이렇게 하면 product.amount를 굳이 할 필요가 없다 (객체간 비교니까)

```kotlin
fun testMultiplication() {
	val five = Dollar(5)
	assertEquals(Dollar(10), five.times(2))
	assertEquals(Dollar(15), five.times(3))
}
```

- 코드를 수정하고 나니 product.amount를 호출하지 않게 되어 amount를 private하게 변경할 수 있게 되었다.

## 검토

- 테스트를 향상시키기 위해서만 개발된 기능을 사용
- 두 테스트가 동시에 실패하면 망한다
    - 동치성에 대한 테스트가 실패하면 곱셈 테스트도 실패한다.
- 위험 요소가 있음에도 계속 진행
    - 자신감 가지고 전진할 수 있을 만큼만 결합의 정도를 낮추기
- 테스트와 코드 사이 결합도를 낮추기 위해 테스트하는 객체의 새 기능을 사용
