# 13장 진짜로 만들기

## 데이터 중복

현재 `Bank`에 있는 가짜 구현 \$10은 테스트 코드에 있는 \$5+\$5와 같다.

```java
Money reduce(Expression source, String to) {
		return Money.dollar(10);
}
```

```java
@Test
public void testSimpleAddition() {
    Money five = Money.dollar(5);
    Expression sum = five.plus(five);
		...
```



조금 불확실한 감이 있긴 하지만 순방향으로 작업해보자.
우선, `Money.plus()`는 그냥 `Money`가 아닌 `Expression(Sum)`을 반환해야 한다.

```java
@Test
public void testPlusReturnsSum() {
    Money five = Money.dollar(5);
    Expression result = five.plus(five);
    Sum sum = (Sum) result;
    assertEquals(five, sum.augend);
    assertEquals(five, sum.addend);
}
```



컴파일하기 위해 Sum 클래스를 만들자

```java
public class Sum implements Expression {
    Money augend;
    Money addend;

    public Sum(Money augend, Money addend) {
    }
}
```

```java
public class Money implements Expression {
  ...
  Expression plus(Money addend) {
        return new Sum(this, addend);
  }
  ...
```



테스트 통과를 위해 `Sum`의 생성자를 수정하자

```java
public class Sum implements Expression {
    Money augend;
    Money addend;

    public Sum(Money augend, Money addend) {
        this.augend = augend;
        this.addend = addend;
    }
}
```



Sum이 가지고 있는 통화 2개와 변환하고 싶은 통화가 모두 같다면 amount를 합친 값을 가진 `Money` 객체여야 한다.

```java
@Test
public void testReduceSum() {
    Expression sum = new Sum(Money.dollar(3), Money.dollar(4));
    Bank bank = new Bank();
    Money result = bank.reduce(sum, "USD");
    assertEquals(Money.dollar(7), result);
}
```

```java
public class Bank {
    Money reduce(Expression source, String to) {
        Sum sum = (Sum) source;
        int amount = sum.augend.amount + sum.addend.amount;
        return new Money(amount, to);
    }
}
```



현재 2가지 이유로 `Bank` 코드가 지저분하다.

1. 캐스팅. 이 코드는 모든 Expression에 대해 작동해야 한다.
   - `Sum sum = (Sum) source`
2. public 필드와 그 필드들에 대한 두 단계에 걸친 레퍼런스
   - `sum.augend.amount`



### 두 단계에 걸친 레퍼런스 제거하기

함수 내용을 `Sum`으로 옮기자

```java
public class Bank {
    Money reduce(Expression source, String to) {
        Sum sum = (Sum) source;
        return sum.reduce(to);
    }
}
```

```java
public class Sum implements Expression {
  ...
  public Money reduce(String to) {
      int amount = augend.amount + addend.amount;
      return new Money(amount, to);
  }
 ...
```



### 캐스팅 없애기

`Bank.reduce()`의 인자로 `Money`를 넘기기 위해 테스트를 작성하고 코드를 수정하자

```java
@Test
public void testReduceMoney() {
    Bank bank = new Bank();
    Money result = bank.reduce(Money.dollar(1), "USD");
    assertEquals(Money.dollar(1), result);
}
```

```java
public class Bank {
    Money reduce(Expression source, String to) {
        if (source instanceof Money) return (Money) source;
        Sum sum = (Sum) source;
        return sum.reduce(to);
    }
}
```



클래스를 명시적으로 검사하는 코드가 있을 때에는 항상 다형성을 사용하도록 바꾸는 것이 좋다.

```java
public class Money implements Expression {
		...
    public Money reduce(String to) {
        return this;
    }
	  ...
}
```

```java
public interface Expression {
    Money reduce(String to);
}
```

```java
public class Bank {
    Money reduce(Expression source, String to) {
        return source.reduce(to);
    }
}
```
