# 14장 바꾸기

### 프랑을 달러로 바꾸기

일단 환율은 2:1로 설정하자

```java
@Test
public void testReduceMoneyDifferentCurrency() {
    Bank bank = new Bank();
    bank.addRate("CHF", "USD", 2);
    Money result = bank.reduce(Money.Franc(2), "USD");
    assertEquals(Money.dollar(1), result);
}
```



다음과 같이 코드를 작성하면 테스트를 통과할 수 있다.

```java
public class Money implements Expression {
  ...
	public Money reduce(String to) {
      int rate = (currency.equals("CHF") && currency.equals("USD")) ? 2 : 1;
      return new Money(amount / rate, to);
  }
  ...
}
```



 환율정보는 Bank가 알고 있어야한다. Money에서는 Bank에게 환율을 물어봐야 한다.

```java
public class Bank {
  ...
  Money reduce(Expression source, String to) {
      return source.reduce(this, to);
  }
  
  int rate(String from, String to) {
     return (from.equals("CHF") && to.equals("USD")) ? 2 : 1;
  }
	...
}
```

```java
public interface Expression {
    Money reduce(Bank bank, String to);
}
```

```java
public class Sum implements Expression {
	  ...
  	public Money reduce(Bank bank,  String to) {
        int amount = augend.amount + addend.amount;
        return new Money(amount, to);
    }
	  ...
}
```

```java
public class Money implements Expression {
  ...
	public Money reduce(Bank bank, String to) {
      int rate = bank.rate(currency, to);
      return new Money(amount / rate, to);
  }
  ...
}
```



Bank에서 환율표를 가지고 있다가 필요할 때 찾아볼 수 있게 하고 싶다.

통화와 환율을 매핑시키는 해시 테이블을 사용하자

같은 통화의 경우에는 환율을 1 반환해야 하므로 테스트를 만들자.

```java
@Test
public void testIdentityRate() {
    assertEquals(1, new Bank().rate("USD", "USD"));
}
```

```java
public class Bank {

    private Hashtable rates = new Hashtable();

    Money reduce(Expression source, String to) {
        return source.reduce(this, to);
    }

    int rate(String from, String to) {
        if (from.equals(to)) return 1;
        Integer rate = (Integer) rates.get(new Pair(from, to));
        return rate.intValue();
    }

    void addRate(String from, String to, int rate) {
        rates.put(new Pair(from, to), new Integer(rate));
    }

    private class Pair {
        private String from;
        private String to;

        Pair(String from, String to) {
            this.from = from;
            this.to = to;
        }

        @Override
        public boolean equals(Object object) {
            Pair pair = (Pair) object;
            return from.equals(pair.from) && to.equals(pair.to);
        }

        @Override
        public int hashCode() {
            return 0;
        }
    }
}
```
