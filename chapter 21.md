# 21장

다음으로 구현할 테스트를 선택할때 기준

→ 나에게 뭔가 가르침을 줄 수 있고

→내가 만들 수 있다는 확신이 드는 것

우선 TestCase.run()이

테스트 하나의 실행 결과를 기록하는 TestResult ‘객체’를 반환하게 한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/c71f9d4b-5e52-4bbc-ace3-466b922c70a6)


TestResult 객체를 가짜구현으로 만들어준다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/84fa52fe-548c-4122-9fa9-178a8d1a5843)


그리고 run이 실행될때, TestResult를 결과로 반환한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/ecd6fdb7-5c65-498e-9cb8-9fcc2f90b850)


TestResult는 실제 실행된 테스트 수를 계산한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/4a9aa5a6-6e2c-43e8-aef8-a33ae44b8ec0)


이제 run함수에서 이 메서드를 실제로 호출하게 만들자.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/8620c776-2324-4099-a9ee-5f500a0f4d68)


실패하는 테스트의 수도 변수로 바꾸기 전에, 해당 개수를 측정하는 테스트를 다시 한 번 TestCaseTest에 작성한다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/3fa313af-4132-40c0-a31c-e021901e55ae)


그리고 testBrokenMethod를 구현한다.
![image](https://github.com/KonCC/test-driven-development/assets/102205852/3f0a1ac7-d61b-4504-a594-dc51813a3694)


예외 처리는 잠시 할 일 목록에 남겨두자.

**지금까지 한 일**

-   ~테스트 메서드 호출하기~
-   ~먼저 setUp 호출하기~
-   ~나중에 tearDown 호출하기~
-   테스트 메서드가 실패하더라도 tearDown 호출하기
-   테스트 여러 개 실행하기
-   ~수집한 결과를 출력하기~
-   ~WasRun에 로그 문자열 남기기~

**이번 장에서 우리가 한 일**

-   가짜 구현을 한 뒤 상수를 변수로 단계적으로 바꾸어 실제 구현으로 만들었다.
-   또 다른 테스트를 작성했다.
-   테스트가 실패할 경우 작은 스케일로 또 다른 테스트를 만들어 실패한 테스트를 성공하게 만드는 것을 보조한다.
