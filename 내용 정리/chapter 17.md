# 17장 Money 회고

## 다음에 할 일은 무엇인가

### Sum.plus()와 Money.plus() 사이의 중복 제거

Expression을 클래스로 변환하여 중복 코드를 제거한다.

```java
public class Sum implements Expression {
  ...
	public Expression plus(Expression addend) {
  	  return new Sum(this, addend);
  }
  ...
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



### Code Review 프로그램 실행하기

- 스몰토크의 스몰린트(SmallLint) 같은 코드 감정(code critic) 프로그램을 실행하기
- 자동화된 감정 프로그램은 뭔가 잊어먹는 일이 없기 때문에, 쓸모 없어진 구현을 지우지 않더라도 스트레스 받지 않아도 된다.



### 지금까지 설계한 것을 검토하기

- 할일 목록이 빌 때가 그때까지 설계한 것을 검토하기에 적절한 시기다.



## TDD 주기

1. 작은 테스트를 추가한다.
2. 모든 테스트를 실행하고, 실패하는 것을 확인한다.
3. 코드에 변화를 준다.
4. 모든 테스트를 실행하고, 성공하는 것을 확인한다.
5. 중복을 제거하기 위해 리팩토링한다.



큰 프로젝트에서도 테스트를 통과하기 위해 수정하는 횟수는 충분히 적게 유지된다. 또한 리팩토리당 수정 횟수는 Fat Tail 분포를 따른다.



## 테스트의 질

- TDD의 부산물로 자연히 생기는 테스트와는 별개의 테스트가 필요하다.
  - 성능테스트
  - 스트레스 테스트
  - 사용성 테스트

- 테스트에 대해 널리 사용되는 지표

  - 명령문 커버리지 : TDD는 100% 명령문 커버리지를 따른다.
  - 결함삽입 : 코드의 의미를 바꾼 후에 테스트가 실패하는지 확인

- 테스트 커버리지를 향상시키는 방법

  - 더 많은 테스트 작성하기

  - 프로그램 로직을 단순화하기
