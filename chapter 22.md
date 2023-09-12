# 22장 - 실패 처리하기

# 이전 상황

## WasRun

![스크린샷 2023-09-11 오후 8.28.51.png](https://github.com/KonCC/test-driven-development/blob/main/images/chapter%2022-1.png)

## TestCaseTest

![스크린샷 2023-09-11 오후 8.29.05.png](https://github.com/KonCC/test-driven-development/blob/main/images/chapter%2022-2.png)

- 실패하는 테스트를 좀 더 세밀한 단위의 테스트를 작성해서 올바른 결과를 출력하는 걸 확인하자

---

## Test실패 문자열

- 일단 test 실패 시 문자열이 제대로 나오는지 확인하자
    
    ![스크린샷 2023-09-11 오후 8.33.08.png](https://github.com/KonCC/test-driven-development/blob/main/images/chapter%2022-3.png)
    
    ![스크린샷 2023-09-11 오후 8.33.18.png](https://github.com/KonCC/test-driven-development/blob/main/images/chapter%2022-4.png)
    
    - 횟수는 맞다면 제대로 출력할 수 있지만 일단 신경 쓰지 않는다. (저자가 커피 약발이 들기 시작했기 때문…)
    

## testFailed() 호출하기

- 언제 호출해야 할까
    - 예외를 잡았을 때
    
    ## TestCase
    
    ![스크린샷 2023-09-11 오후 8.41.52.png](https://github.com/KonCC/test-driven-development/blob/main/images/chapter%2022-5.png)
    
    - self.setUp()에서 문제가 발생한 경우는 예외가 잡히지 않을 것
        - 하지만 코드를 수정하기 위해서는 또 다른 테스트가 필요
        - 그건 연습문제..

## 검토

- 작은 스케일의 테스트가 통과하게 만듦 (formatting 메서드)
- 큰 스케일의 테스트를 다시 도입 (testFailed)
- 작은 스케일의 테스트에서 보았던 메커니즘을 이용하여 큰 스케일의 테스트를 빠르게 통과 (횟수가 맞게 출력될 거라고 생각하고 넘어가기)
- 중요한 문제를 발견했는데 이를 바로 처리하기보다는 할일 목록에 적어놓음 (self.setUp에서 예외가 발생한다면?)