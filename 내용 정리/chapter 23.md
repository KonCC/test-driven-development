# 23장 - 얼마나 달콤한지

![스크린샷 2023-09-11 오후 8.47.20.png](./images/chapter%2023-1.png)

파일 마지막에 테스트를 호출하는 코드가 중복이 많다.

- 테스트를 한 번에 모아서 실행할 수 있는 기능을 원함
- TestSuite를 구현

![스크린샷 2023-09-11 오후 8.49.48.png](./images/chapter%2023-2.png)

- add메서드가 필요

![스크린샷 2023-09-11 오후 8.52.12.png](./images/chapter%2023-3.png)

- test.run()에서 TestCase.run() 메서드에 매개변수가 추가되면 여기도 매개 변수를 추가해줘야 한다.
    - 파이썬의 기본 매개 변수 기능을 사용
        - 기본값은 컴파일타임에 평가되므로 TestResult 재사용 불가
    - 메서드를 두 부분으로 나눈다.
        - TestResult를 할당하는 부분과 TestResult를 가지고 테스트를 수행하는 부분
        - 두 부분에 대한 좋은 이름이 떠오르지 않음 → 별로 좋은 전략이 아니다
    - 호출하는 곳에서 TestResults를 할당한다.
        - 매개 변수 수집 패턴이라 부른다.
    
    ## TestCaseTest
    
    ![스크린샷 2023-09-11 오후 8.58.01.png](./images/chapter%2023-4.png)
    
    - suite.run에 만들어 놓은 TestResult를 전달한다.
    
    ## TestSuite
    
    ![스크린샷 2023-09-11 오후 8.58.14.png](./images/chapter%2023-5.png)
    
    - run은 이제 반환하지 않아도 된다.
    
    ## TestCase
    
    ![스크린샷 2023-09-11 오후 8.58.27.png](./images/chapter%2023-6.png)
    
    - 첫번째 줄에 result = TestResult()부분을 지울 수 있게 되었따.

- 그리고 이제 테스트 호출 코드를 정리할 수 있다.

![스크린샷 2023-09-11 오후 9.02.10.png](./images/chapter%2023-7.png)

- 실패하는 테스트 고치기
- test.run() 메서드에 result 매개변수가 없어 실패하는 메서드를 통과하게 수정해주자
    
    ![스크린샷 2023-09-11 오후 9.08.31.png](./images/chapter%2023-8.png)
    
    - result = TestResult()가 중복되고 있다
        - setUp()에서 생성하게 만들기
            
            ![스크린샷 2023-09-11 오후 9.13.23.png](./images/chapter%2023-9.png)
            
        
    
    # 검토
    
    - TestSuite를 위한 테스트 작성
    - 테스트를 통과시키지 못한 채 일부분만 구현
    - run 메서드의 인터페이스 변경
    - 공통된 셋업 코드를 분리
    
    # 전체 코드

  ```
  class TestCase:
    def __init__(self,name):
        self.name = name
    def setUp(self):
        self.wasRun = None
        self.wasSetUp = 1
    def run(self):
        result.testStarted()
        self.setUp()
        try:
            method = getattr(self, self.name)
            method()
        except:
            result.testFailed()
        self.tearDown()
        return result
    def tearDown(self):
        pass

  class WasRun(TestCase):
      def testMethod(self):
          self.wasRun = 1
          self.log = self.log + "testMethod "
      def setUp(self):
          self.wasRun = None
          self.wasSetUp = 1
          self.log = "setUp "
      def tearDown(self):
          self.log = self.log + "tearDown "
      def testBrokenMethod(self):
          raise Exception
  
  class TestCaseTest(TestCase):
      def setUp(self):
          self.result = TestResult()
      def testTemplateMethod(self):
          test = WasRun("testMethod")
          test.run(self.result)
          assert("setUp testMethod tearDown " == test.log)
      def testResult(self):
          test = WasRun("testMethod")
          test.run(self.result)
          assert("1 run, 0 failed" == result.summary())
      def testFailedResult(self):
          test = WasRun("testBrokenMethod")
          test.run(self.result)
          assert("1 run, 1 failed" == result.summary())
      def testFailedResultFormatting(self):
          result = TestResult()
          result.testStarted()
          result.testFailed()
          assert("1 run, 1 failed" == result.summary())
      def testSuite(self):
          suite = TestSuite()
          suite.add(WasRun("testMethod"))
          suite.add(WasRun("testBrokenMethod"))
          suite.run(self.result)
          assert("2 run, 1 failed" == result.summary())
  
  class TestResult:
      def __init__(self):
          self.runCount = 0
          self.failureCount = 0
      def testStarted(self):
          self.runCount = self.runCount + 1
      def testFailed(self):
          self.failureCount = self.failureCount + 1
      def summary(self):
          return "%d run, %d failed" % (self.runCount, self.failureCount)
      
  
  class TestSuite:
      def __init__(self):
          self.tests = []
      def add(self, test):
          self.tests.append(test)
      def run(self, result):
          for test in self.tests:
              test.run(result)
          
          
  suite = TestSuite()
  suite.add(TestCaseTest("testTemplateMethod"))
  suite.add(TestCaseTest("testResult"))
  suite.add(TestCaseTest("testFailedResultFormatting"))
  suite.add(TestCaseTest("testFailedResult"))
  suite.add(TestCaseTest("testSuite"))
  result = TestResult()
  suite.run(result)
  print result.summary()

```
