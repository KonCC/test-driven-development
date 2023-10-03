# 8장 객체 만들기

##### 하위 클래스에 대한 참조 줄이기

## Factory Method를 도입해서 하위 클래스에 대한 직접적인 참조를 줄인다.

1. TestCode 수정
![img](../images/chapter%208-1.png)  
2. 기본 코드 수정
![img](../images/chapter%208-2.png)
3. 에러-times()가 Money에 정의되지 않음
4. 에러 수정 & 팩토리 메소드 나머지 코드에 모두 적용
![img](../images/chapter%208-3.png)
## Before & After

![img](../images/chapter%208-4.png)
