# 21장

다음으로 구현할 테스트를 선택할때 기준

→ 나에게 뭔가 가르침을 줄 수 있고

→내가 만들 수 있다는 확신이 드는 것

우선 TestCase.run()이

테스트 하나의 실행 결과를 기록하는 TestResult ‘객체’를 반환하게 한다.

[##_Image|kage@bojnm0/btssS3bP0ud/bJ02BTFCkdKjHFfIkyebak/img.png|CDM|1.3|{"originWidth":584,"originHeight":122,"style":"alignCenter"}_##]

TestResult 객체를 가짜구현으로 만들어준다.

[##_Image|kage@bQGp4c/btssVWvYcrS/cHUd5cNfB9ewvlhKGJcyy0/img.png|CDM|1.3|{"originWidth":319,"originHeight":67,"style":"alignCenter"}_##]

그리고 run이 실행될때, TestResult를 결과로 반환한다.

[##_Image|kage@boyp3A/btss71iTJYY/94Rz7UUNKJClkcKZCXtcY1/img.png|CDM|1.3|{"originWidth":444,"originHeight":195,"style":"alignCenter"}_##]

TestResult는 실제 실행된 테스트 수를 계산한다.

[##_Image|kage@b6WGjV/btssS1ygkkH/oi6995Ds5krf198i7zCPMK/img.png|CDM|1.3|{"originWidth":466,"originHeight":230,"style":"alignCenter"}_##]

이제 run함수에서 이 메서드를 실제로 호출하게 만들자.

[##_Image|kage@wXxxR/btss9AemlLN/1jGrPnKGXzRQY1WrVrEK5k/img.png|CDM|1.3|{"originWidth":366,"originHeight":220,"style":"alignCenter"}_##]

실패하는 테스트의 수도 변수로 바꾸기 전에, 해당 개수를 측정하는 테스트를 다시 한 번 TestCaseTest에 작성한다.

[##_Image|kage@FjzQW/btss9BqN6AU/CqokWswocdfJs9uhM9AwaK/img.png|CDM|1.3|{"originWidth":464,"originHeight":113,"style":"alignCenter"}_##]

그리고 testBrokenMethod를 구현한다.

[##_Image|kage@pxKnB/btssTuHccBh/kqig3kbV5yhZCofnNTS3H1/img.png|CDM|1.3|{"originWidth":275,"originHeight":81,"style":"alignCenter"}_##]

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
