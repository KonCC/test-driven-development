# 15장 서로 다른 통화 더하기

$5 +10CHF에 대한 테스트 코드를 작성한다.

```java
@Test
public void testMixedAddition() {
    Money fiveBucks = Money.dollar(5);
    Money tenFrances = Money.Franc(10);
    Bank bank = new Bank();
    bank.addRate("CHF", "USD", 2);
    Money result = bank.reduce(fiveBucks.plus(tenFrances), "USD");
    assertEquals(Money.dollar(10), result);
}
```



테스트가 실패하는데, 이는 `Sum`에서 인자들을 축약(reduce)하지 않았기 때문에 생기는 문제이다.

```java
public class Sum implements Expression {
	...
  public Money reduce(Bank bank, String to) {
      int amount = augend.reduce(bank, to).amount 
        		+ addend.reduce(bank, to).amount;
      return new Money(amount, to);
  }
	...
```



### 인터페이스에 의존하기

Money를 Expression로 대체하자

```java
public class Sum implements Expression {
    Expression augend;
    Expression addend;

    public Sum(Expression augend, Expression addend) {
        this.augend = augend;
        this.addend = addend;
    }
		...
}

```

```java
public class Money implements Expression {
    ...
    Expression times(int multiplier) {
        return new Money(amount * multiplier, currency);
    }

    Expression plus(Expression addend) {
        return new Sum(this, addend);
    }
		...
}
```





Expression은 `plus()`와 `times()` 오퍼레이션을 지원해야 한다.

```java
public void testMixedAddition() {
    Expression fiveBucks = Money.dollar(5);
    Expression tenFrances = Money.Franc(10);
    Bank bank = new Bank();
    bank.addRate("CHF", "USD", 2);
    Money result = bank.reduce(fiveBucks.plus(tenFrances), "USD");
    assertEquals(Money.dollar(10), result);
}
```

```java
public interface Expression {
    Money reduce(Bank bank, String to);
    Expression plus(Expression addend); // 추가
}
```

```java
public class Money implements Expression {
    ...
    public Expression plus(Expression addend) {
        return new Sum(this, addend);
    }
  	...
}
```

```java
public class Sum implements Expression {
    ...
    public Expression plus(Expression addend) {
        return null;
    }
}
```

