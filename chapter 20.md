# 20장

setUp은 tc가 실행되기 전에 호출되어야 하고,

tearDown은 tc가 실행된 후에 호출되어야 한다.

항상 로그의 끝부분에만 기록을 추가하면 메서드 호출 순서를 알 수 있을 것.

[##_Image|kage@7cmer/btssUauGedO/vIVP9bDKp1oLnWnOb57W3K/img.png|CDM|1.3|{"originWidth":364,"originHeight":173,"style":"alignCenter"}_##]

testSetUp 메서드가 플래그 대신 로그를 검사하도록 변경 → wasSetUp 플래그를 지울 수 있어졌다.

[##_Image|kage@d0S4TW/btssS0MUOJu/fn6S6akLaNSk3olhAFP0jk/img.png|CDM|1.3|{"originWidth":426,"originHeight":124,"style":"alignCenter"}_##]

이 테스트가 두개의 테스트가 할일을 모두 수행하므로 testRunning을 지우고 testSetUp의 이름을 바꿔준다.

[##_Image|kage@cADkGL/btssVOkD9PW/oH1wrYEIkE5okKMo7MksO0/img.png|CDM|1.3|{"originWidth":455,"originHeight":144,"style":"alignCenter"}_##]

wasRun의 인스턴스를 한곳에서만 사용하므로 다시 분리했던 setUp을 합친다

[##_Image|kage@vSBe3/btssS2D02WT/UgkvlTJrFYQa6vhB4GyBZK/img.png|CDM|1.3|{"originWidth":509,"originHeight":139,"style":"alignCenter"}_##]

~테스트 메서드 호출하기~

~먼저 setUp 호출하기~

**나중에 tearDown 호출하기**

테스트 메서드가 실패하더라도 tearDown 호출하기

테스트 여러 개 실행하기

수집한 결과를 출력하기

~WasRun에 로그 문자열 남기기~

이제 tearDown()을 구현..이 아닌 테스트를 해보자.

[##_Image|kage@QLlPy/btss84TYLjL/jPWYcxtGfbQD4FEniv1Fg1/img.png|CDM|1.3|{"originWidth":605,"originHeight":150,"style":"alignCenter"}_##]

test앞에 self 를 붙인거랑 뭐가달라지는거지

실패한다. 다음과 같이 수정하자.

[##_Image|kage@0YaZd/btssUHlxO2y/gzhjhpNrH1oKpzluHU7Qkk/img.png|CDM|1.3|{"originWidth":403,"originHeight":143,"style":"alignCenter"}_##][##_Image|kage@TcMNv/btss3MlVi1Z/fKIbCkJL8of7aRm7JL7Xt1/img.png|CDM|1.3|{"originWidth":401,"originHeight":280,"style":"alignCenter"}_##]

지금까지 한일

-   플래그에서 로그로 테스트 전략을 구조 조정
-   새로운 로그 기능을 이용하여 tearDown()을 테스트하고 구현
-   문제를 발견하고 뒤로 돌아가는 대신 수정
