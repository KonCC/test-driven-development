# 2장 타락한 객체

현재까지 짠 코드에서는 Dollar에 대한 연산을 수행하고 나면 Dollar의 값이 바뀌고 만다.

다음 테스트를 살펴보자.

```java
 public void testMultiplication() {
     Dollar five = new Dollar(5);
     five.times(2);
     assertEquals(10, five.amount);
     five.times(3);
     assertEquals(15, five.amount);
 }
```

한번 times를 실행하고 나면, 객체는 값이 바뀌고 오염되므로, 새로운 객체를 반환하기를 원한다.

```java
 public void testMultiplication() {
     Dollar five = new Dollar(5);
     Dollar product = five.times(2);
     assertEquals(10, product.amount);
     product = five.times(3);
     assertEquals(15, product.amount);
 }
```

이렇게 수정할 경우, 수량에 따른 개수를 계산은 product 객체에 위임하게 되므로, five 객체는 오염되지 않을 수 있다.

하지만 기존 코드로는 컴파일이 안되므로 ,  times를 수정해주자.

```java
 Dollar times(int multiplier) {
     amount *= multiplier;
     return null;
 }
```

이제 컴파일은 성공하지만, 실행은 되지 않는다.

올바른 값을 반환해 테스트를 통과하게 해주자.

```java
 Dollar times(int multiplier) {
     return new Dollar(amount*multiplier);
 }
```

이제 테스트는 통과했고, 테스트 두개를 무사히 해결했다.

- $5 + 10CHF = $10 (환율이 2:1일 경우)
- ~$5 X 2 = $ 10 (가지고 있는 주식 수 만큼 가격 계산)~
- amount를 private으로 만들기
- ~Dollar 부작용?~
- money 반올림?

지금까지 해온 TDD의 흐름은 다음과 같다.

- 설계상의 결함을 그 결함으로 인해 실패하는 테스트로 변환했다.
- 스텁 구현으로 빠르게 컴파일을 통과하도록 했다.
- 올바르다고 생각하는 코드를 입력해 테스트를 통과한다.
