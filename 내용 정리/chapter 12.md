# 13장 드디어 더하기

## 다중 통화를 표현하는 방법

1. 모든 내부 값을 참조통화로 전환하는 방법 – 여러 환율을 쓰기 어려움

2. 외부 구현은 같으면서 내부 구현은 다른 객체(imposter)를 만들어서 사용
    - Money와 비슷하게 동작하지만, 두 Money의 합을 나타내는 객체를 만드는 것
    1. Money의 합을 지갑처럼 취급하는 방법
        - 금액과 통화가 다른 여러 화폐가 Money에 들어갈 수 있음
    2. Money의 합을 수식으로 취급하는 방법 ($2 + 3CHF) * 5
        - Money를 수식의 가장 작은 단위로 볼 수 있음
        - 연산의 결과로 Expression이 생기고 그 중 하나는 sum임
        - 연산이 완료되면 환율을 이용해서 Expression을 단일 통화로 축약할 수 있음

-  Reduced는 Expression으로 Expression에 환율을 적용함으로써 얻어진다
- Bank가 reduce의 책임을 가짐
![img](../images/chapter%2012-1.png)


> 왜 Bank에서 reduce에 대한 책임을 가지나?  
A) 핵심 객체인 Expression이 가능한 오랫 동안 유연하게 하기 위해서
>+ 테스트하기 쉽고, 재활용 & 이해가 쉬움
>+ 추가 되는 기능을 생각하면 Expression에 몰릴 가능성이 있음  
> -\> Expression이 다른 부분에 대해서는 모르도록 해야함

일단은 reduce에 대해 스텁 구현을 해놓음 
![img](../images/chapter%2012-2.png)

>결과적으로는, 컴파일이 가능하며  
testCode가 전부 초록색임  
즉, 리팩토링할 수 있음

