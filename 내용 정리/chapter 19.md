# 19장 테이블 차리기

테스트를 작성할 때 공통된 3A 패턴

-   준비 - 객체를 생성한다.
-   행동 - 어떤 자극을 준다.
-   확인 - 결과를 검사한다.

성능 - 여러 테스트가 같은 객체를 사용한다면, 하나만 생성해서 공유할 수 있을 것

격리 - 한 테스트에서의 성공유무가 다른 테스트에 영향을 주지 않기를 원한다.

객체를 공유하는 상태에서 하나의 테스트가 객체 상태를 변경한다면 다른 테스트 결과에 영향을 미칠 가능성이 존재.

테스트를 실행하기전 객체를 생성한 것을 확인하는 플래그를 세운다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/dd90b8d5-a346-4395-9a52-b24c93b26a7d)
![image](https://github.com/KonCC/test-driven-development/assets/102205852/3d48257a-3565-475d-ba9b-bc751adc2aa7)



WasRun의 setUp을 호출해야하므로, 그 일은 TestCase에서 하도록 한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/3f8b4509-098c-4d0f-b049-84243f73bb73)


이렇게 할 경우 오버라이드한 setUp 함수가 실행되면서 wasSetUp 값이 설정된다.

테스트를 실행하기 전에 플래그를 검사하지 않도록 단순화한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/8911c96f-5933-4c80-ab52-88a40df52fb7)


각각의 테스트는 WasRun 인스턴스를 생성해서 사용하게 된다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/4d1a212e-0c9d-4d7a-98b8-b431e05fac13)


이번 장에서 한 일

-   테스트를 작성하는데에 간결함이 성능 향상보다 중요하다 생각하기
-   setUp()을 테스트하고 구현하기
-   예제 TC를 단순화하기 위해 setUp 사용
-   예제 TC에 대한 TC를 단순화하기 위해 setUp 사용. ?

~테스트 메서드 호출하기~

~먼저 setUp 호출하기~

나중에 tearDown 호출하기

테스트 메서드가 실패하더라도 tearDown 호출하기

테스트 여러 개 실행하기

수집한 결과를 출력하기
