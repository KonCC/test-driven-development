# 1장 다중 통화를 지원하는 Money 객체

TDD의 리듬

1.  재빨리 테스트를 하나 추가 (가짜로 구현)
2.  모든 테스트를 실행하고, 새로 추가한 것의 실패 여부 확인
3.  코드 수정
4.  모든 테스트를 실행하고, 전부 성공하는지 확인
5.  리팩토링을 통한 중복 제거



다음과 같은 MONEY 객체가 있다고 가정해보자.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/23f2ef03-0350-4793-8105-24509924ca16)


이를 다중 통화를 지원하는 보고서를 만들기 위해선 통화 단위를 추가하는 등 수정이 불가피하다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/f96b148f-2334-4798-992c-9cbb0f3b3880)


**객체를 만들면서 시작하는 것이 아닌 테스트를 먼저 만들어야 한다.**

가장 빨리 간단한 테스트를 위해, 주식 개수만큼 값을 곱해 금액을 구하는 함수를 만들어보자 .

```java
 public void testMultiplication() {
     Dollar five = new Dollar(5);
     five.times(2);
     assertEquals(10, five.amount);
 }
```

위 코드를 작성할 때 다음과 같은 부분들을 생각해야 한다.

- $5 + 10CHF = $10 (환율이 2:1일 경우)
- $5 X 2 = $ 10 (가지고 있는 주식 수 만큼 가격 계산)
- amount를 private으로 만들기
- Dollar 부작용?
- money 반올림?

그리고 위 코드를 실행하면 다음 컴파일 에러들이 발생한다.

- Dollar 클래스가 없음
- 생성자가 없음
- times(int) 메소드가 없음
- amount 필드가 없음

우선 빨간 막대를 빠르게 보기 위해, 컴파일 에러부터 해결한다.

```java
 public class Dollar {
     int amount;
     
     Dollar(int amount) {
     }
     
     void times(int multiplier) {
     }
 }
```

테스트를 실행하면, 결과로 10이 나와야 하지만 0이 나오기 때문에, 빨간 막대를 보게 된다.

최소한의 작업으로 초록 막대를 보려면 다음과 같이 수정한다.

```java
 int amount = 10;
```

1.  재빨리 테스트를 하나 추가 (가짜로 구현)
2.  모든 테스트를 실행하고, 새로 추가한 것의 실패 여부 확인
3.  코드 수정
4.  모든 테스트를 실행하고, 전부 성공하는지 확인
5.  리팩토링을 통한 중복 제거

이제 위 과정중 4번까지 성공한다.

그렇다면 리팩토링을 통해 중복을 제거해보자.

중복은 도대체 어디서 발생한 것일까?

```java
 int amount = 5 * 2
```

10을 5 \* 2로 바꾸면 중복이 보인다. 5와 2라는 데이터가 테스트 코드와 클래스에 중복이 되는 것이다.

이를 제거하기 위해 생성자와 times를 새롭게 정의하자.

```java
 public class Dollar {
     int amount;

     Dollar(int amount) {
         this.amount = amount;
     }

     void times(int multiplier) {
         amount *= multiplier;
     }
 }
```

이제 중복은 제거되고, 첫번째 테스트는 완벽히 통과되었다.

- $5 + 10CHF = $10 (환율이 2:1일 경우)
- ~$5 X 2 = $ 10 (가지고 있는 주식 수 만큼 가격 계산)~
- amount를 private으로 만들기
- Dollar 부작용?
- money 반올림?

지금까지 한 작업은 다음과 같다.

- 알고 있는, 작업해야 할 테스트 목록 만들기
- 오퍼레이션이 외부에서 어떻게 보이길 원하는지 코드로표현
- junit 상세 사항무시
- 스텁 구현(구현되지 않은 함수 임의 생성)을 통해 테스트 컴파일
- 끔찍한 구현(하드 코딩) 을 통해 테스트 통과
- 상수를 변수로 변경하며 점진적 일반화
- 새로운 할일들을 처리하는 대신 할 일 목록에 추가하고 넘어가기
