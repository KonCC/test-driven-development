# 2부

xUnit이란?

이 책의 저자 켄트 백이 고안한 프레임워크인 Sunit으로부터 기능과 구조를 착안한,

unit testing framework를 통틀어 칭하는 명칭이다.

파생상품으로는 Junit, Nnuit, [xUnit.net](http://xUnit.net) 등이 있다.

# 18장

## xUnit으로 가는 첫걸음

2부의 주제

-   TDD를 통해 실제 소프트웨어를 만드는 발전된 예제
-   자기 참조 프로그래밍에 대한 전산학 실습

이번 장에서 할 일

테스트 프레임워크를 테스트 주도 개발로 만들기.

-   테스트 메서드 호출하기
-   먼저 setUp 호출하기
-   나중에 tearDown 호출하기
-   테스트 메서드가 실패하더라도 tearDown 호출하기
-   여러 개의 테스트 실행하기
-   수집된 결과를 출력하기

테스트 메서드가 호출되면 true를 반환하는 원시테스트 작성

[##_Image|kage@dAlFPY/btssS3ixvLK/mV4BGOB4UVKskjQJaQJQAk/img.png|CDM|1.3|{"originWidth":359,"originHeight":181,"style":"alignCenter"}_##]

책에서는 testMethod를 정의해야 할 때 그 사실을 알아채고 스텁을 자동으로 생성해주면 얼마나 좋을까 하는데 , 코파일럿이 실제로 해준다.. 좋은 세

테스트 메서드를 직접 호출하는 대신 진짜 인터페이스인 run 메서드를 사용한다.

[##_Image|kage@u8aKW/btssUPjskge/RiQrylNkc0KJErEZuAWRk1/img.png|CDM|1.3|{"originWidth":494,"originHeight":392,"style":"alignCenter"}_##]

테스트메서드를 동적 호출

**getattr** 함수를 사용하면 함수를 변수에 저장할 수 있다.

[##_Image|kage@dWgUGz/btssT66TBs1/ZvNvKadxlvfO1sEueuuuA1/img.png|CDM|1.3|{"originWidth":477,"originHeight":307,"style":"alignCenter"}_##]

### 현재 WasRun 클래스가 수행하는 일 두가지

-   메서드가 호출되었는지 아닌지 기억하는 일
-   메서드를 동적으로 호출하는 일

WasRun은 독립된 두가지 일을 수행하므로, TestCase 상위 클래스를 만들고 이를 상속받도록 한다.

[##_Image|kage@Q1Bdv/btss3YmLuiL/kfa0Kv5LJGaJdPzbxyrOVK/img.png|CDM|1.3|{"originWidth":284,"originHeight":79,"style":"alignCenter"}_##][##_Image|kage@dMoKcw/btssVXhIIle/BxeMfUVR15vVy7c9Q8Rqc1/img.png|CDM|1.3|{"originWidth":346,"originHeight":147,"style":"alignCenter"}_##]

run 메서드는 상위 클래스 속성만을 사용하므로 이 또한 상위 클래스로 옮겨주고 상속받아 사용한다.

[##_Image|kage@c3v9CG/btssUKWQdGw/bc6FupIZqHtJTeUaUo7aF1/img.png|CDM|1.3|{"originWidth":546,"originHeight":222,"style":"alignCenter"}_##]

테스트 코드를 클래스로 새로 작성한다.

[##_Image|kage@brv6d2/btssUceSYxG/9YB1mVzkF45zTERQEmzz51/img.png|CDM|1.3|{"originWidth":451,"originHeight":307,"style":"alignCenter"}_##]

~테스트 메서드 호출하기~

먼저 setUp 호출하기

나중에 tearDown 호출하기

테스트 메서드가 실패하더라도 tearDown 호출하기

테스트 여러 개 실행하기

수집한 결과를 출력하기
