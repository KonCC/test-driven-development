## 3장 모두를 위한 평등

객체의 값(정확히는 amount) 를 비교해야 하기 때문에 equals 구현  
모든 인스턴스 변수들이 그렇듯이 amount를 private로 만들기 위해 필요.

Dollar를 해시 테이블의 키로 쓸 경우엔 , hashCode()도 구현 필요.  
(다만, 바로 작업하지 않고 할일 목록에 적어둔다.)

### 테스트 코드 작성 

```
public void testEquality() {
	assertTrue(new Dollar(5).equals(new Dollar(5)));
}
```

### 빨간 막대 제거를 위한 가짜 구현

```
public boolean equals(Object object) {
	return true;
}
```

### 삼각 측량이란 ? 

쉽게 말해 예제가 두개 이상 있어야지만 코드를 일반화 할 수 있다는 것.
$5 == $5 로 true 만 검사하는 것이 아니라
$5 != $6와 같이 false 도 검사할 필요가 있다.

```
public void testEquality() {
	assertTrue(new Dollar(5).equals(new Dollar(5)));
    assertFalse(new Dollar(5).equals(new Dollar(6)));
}
```

### equality 일반화

```
public boolean equals(Object object) {
	Dollar dollar = (Dollar) object;
	return amount == dollar.amount;
}
```

동일성 문제는 일시적으로 해결했으나,
널 값이나 다른 객체와 비교할 때는 해결 x
따라서 할일 목록에 다음 추가

- Equal null
- Equal objcet

### 이 장에서 한 작업들 검토

- 오퍼레이션을 테스트로 작성했다.
- 오퍼레이션을 간단히 구현했다. (항상 true를 반환하는 스텁)
- 곧장 리팩토링 하는 대신 테스트를 좀 더 보완했다.
- 두 경우를 모두 수용할 수 있도록 리팩토링했다.
