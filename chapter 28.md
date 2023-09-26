# 28장. 초록 막대 패턴
## 깨진 테스트 고치기

### 가짜로 구현하기(진짜로 만들기 전까지만)
-	실패하는 테스트를 만들었다면, 상수를 반환하게 만들어라
-	테스트가 통과하면 단계적으로 상수를 변수로 변경(리펙토링)하라
가짜로 구현하기의 2가지 효과
심리학적 효과 : 확신을 갖고 거기부터 리펙토링 할 수 있다
범위 조절 효과 : 현재의 문제에만 집중하도록 해준다
+ 리펙토링이 끝나면 기존이 가짜 코드는 다 사라져있을 것이다

### 삼각측량
-	예가 2개 이상일 때만 삼각측량법을 이용해서 추상화하라
-	어떻게 해야 올바르게 추상화 할 수 있을지 모르겠을 떄 사용하는 방식이다
-	그 외의 경우라면 명백한 구현이나 가짜로 구현하기에 의존하자

### 명백한 구현
-	뭘 해야할 지 알고, 그걸 재빨리 할 수 있다면 그냥 해버려라
-	‘제대로 동작하는’과 ‘깨끗한 코드’를 해결하는 것을 한번에 하기 힘들다면 ‘제대로 동작하는’부터 해결하고 ‘깨끗한 코드’를 해결하라
-	손가락이 머리를 따라오지 못하면 앞의 방식으로 해결하라
-	(코드가 생각하는 대로 짜지지 않으면, 가짜 구현하기나 삼각 측량을 사용하라)
+ 컬렉션은 그냥 뭐 계속 해왔던 것처럼 - 일단은 컬렉션 없이 구현하고, 그 다음에 컬렉션을 사용하도록 구현 함