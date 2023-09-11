# 16장 드디어, 추상화

`Sum.plus()` 를 테스트하고 구현하자

```java
public void testSumPlusMoney() {
    Expression fiveBucks = Money.dollar(5);
    Expression tenFrances = Money.Franc(10);
    Bank bank = new Bank();
    bank.addRate("CHF", "USD", 2);
    Expression sum = new Sum(fiveBucks, tenFrances).plus(fiveBucks);
    Money result = bank.reduce(sum, "USD");
    assertEquals(Money.dollar(15), result);
}
```

```java
public class Sum implements Expression {
    ...
    public Expression plus(Expression addend) {
        return new Sum(this, addend);
    }
	  ...
}
```



`Sum.times()`을 만들기 위해 테스트를 작성하고 수정

```java
public void testSumTimes() {
    Expression fiveBucks = Money.dollar(5);
    Expression tenFrances = Money.Franc(10);
    Bank bank = new Bank();
    bank.addRate("CHF", "USD", 2);
    Expression sum = new Sum(fiveBucks, tenFrances).times(2);
    Money result = bank.reduce(sum, "USD");
    assertEquals(Money.dollar(20), result);
}
```

```java
public interface Expression {
    Money reduce(Bank bank, String to);
    Expression plus(Expression addend);
    Expression times(int multiplier);
}
```

```java
public class Money implements Expression {
  ...
	public Expression times(int multiplier) {
  	    return new Money(amount * multiplier, currency);
   ...
}
```

```java
public class Sum implements Expression {
  ...
	public Expression times(int multiplier) {
  	  return new Sum(augend.times(multiplier), addend.times(multiplier));
  }
  ...
```



\$5 + \$5를 할 때에 Money를 반환하는 것을 테스트해보기

```java
public void testPlusSameCurrencyReturnsMoney() {
    Expression sum = Money.dollar(1).plus(Money.dollar(1));
    assertTrue(sum instanceof Money);
}
```

하지만 인자가 Money일 경우에(그리고 그 경우에만) 인자의 통화를 확인하는 분명하고 깔끔한 방법이 없으므로 테스트를 삭제한다.
