# 20장 뒷정리하기

setUp은 tc가 실행되기 전에 호출되어야 하고,

tearDown은 tc가 실행된 후에 호출되어야 한다.

항상 로그의 끝부분에만 기록을 추가하면 메서드 호출 순서를 알 수 있을 것.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/4fe86f6c-413c-45c7-b2ad-16b30ec2e39b)


testSetUp 메서드가 플래그 대신 로그를 검사하도록 변경 → wasSetUp 플래그를 지울 수 있어졌다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/dae518c6-2d2e-4722-a1c2-d2e3b3cf874f)


이 테스트가 두개의 테스트가 할일을 모두 수행하므로 testRunning을 지우고 testSetUp의 이름을 바꿔준다.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/adf05412-efea-4964-aa71-7e30d80d969a)


wasRun의 인스턴스를 한곳에서만 사용하므로 다시 분리했던 setUp을 합친다

![image](https://github.com/KonCC/test-driven-development/assets/102205852/572ec267-fdab-4dd0-867a-bbeec6acf218)


~테스트 메서드 호출하기~

~먼저 setUp 호출하기~

**나중에 tearDown 호출하기**

테스트 메서드가 실패하더라도 tearDown 호출하기

테스트 여러 개 실행하기

수집한 결과를 출력하기

~WasRun에 로그 문자열 남기기~

이제 tearDown()을 구현..이 아닌 테스트를 해보자.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/5e0c9342-1972-42d1-a9df-c8629e47c5b7)


test앞에 self 를 붙인거랑 뭐가달라지는거지

실패한다. 다음과 같이 수정하자.

![image](https://github.com/KonCC/test-driven-development/assets/102205852/8cdeedee-3295-4474-b640-110386296268)
![image](https://github.com/KonCC/test-driven-development/assets/102205852/2048953c-0f1f-4b6f-897d-66d95a92955b)



지금까지 한일

-   플래그에서 로그로 테스트 전략을 구조 조정
-   새로운 로그 기능을 이용하여 tearDown()을 테스트하고 구현
-   문제를 발견하고 뒤로 돌아가는 대신 수정
