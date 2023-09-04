# 19장

## 테이블 차리기

테스트를 작성할 때 공통된 3A 패턴

-   준비 - 객체를 생성한다.
-   행동 - 어떤 자극을 준다.
-   확인 - 결과를 검사한다.

성능 - 여러 테스트가 같은 객체를 사용한다면, 하나만 생성해서 공유할 수 있을 것

격리 - 한 테스트에서의 성공유무가 다른 테스트에 영향을 주지 않기를 원한다.

객체를 공유하는 상태에서 하나의 테스트가 객체 상태를 변경한다면 다른 테스트 결과에 영향을 미칠 가능성이 존재.

테스트를 실행하기전 객체를 생성한 것을 확인하는 플래그를 세운다.

[##_Image|kage@bJcR9I/btss9hyUIEM/8HklrQwMfZGKZErxCwHSkK/img.png|CDM|1.3|{"originWidth":343,"originHeight":119,"style":"alignCenter"}_##][##_Image|kage@UbzSi/btssYQWtyIS/2sl7O4gxv5ksYNiAg9p5Tk/img.png|CDM|1.3|{"originWidth":309,"originHeight":110,"style":"alignCenter"}_##]

WasRun의 setUp을 호출해야하므로, 그 일은 TestCase에서 하도록 한다.

[##_Image|kage@zxs4I/btss3HEWzkA/fWGWKwviVqpJpkxRM1ECz0/img.png|CDM|1.3|{"originWidth":479,"originHeight":221,"style":"alignCenter"}_##]

이렇게 할 경우 오버라이드한 setUp 함수가 실행되면서 wasSetUp 값이 설정된다.

테스트를 실행하기 전에 플래그를 검사하지 않도록 단순화한다.

[##_Image|kage@bvgl70/btssTeEms6U/zwCOZo9KNgYQxuyUt2bsGk/img.png|CDM|1.3|{"originWidth":395,"originHeight":145,"style":"alignCenter"}_##]

각각의 테스트는 WasRun 인스턴스를 생성해서 사용하게 된다.

[##_Image|kage@df9OSS/btss86K0SvO/YHbvHbhRlua9lKODVtth2k/img.png|CDM|1.3|{"originWidth":453,"originHeight":343,"style":"alignCenter"}_##]

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
