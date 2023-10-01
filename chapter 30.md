# 30장. 디자인 패턴



## 커맨드

> 계산 작업에 대한 호출을 메시지가 아닌 객체로 표현한다.

- 간단한 메서드 호출보다 복잡한 형태의 계산 작업에 대한 호출이 필요할 땐, 계산 작업에 대한 객체를 생성하여 이를 호출하면 된다.
- 복잡한 계산 작업 호출은 값비싼 메커니즘을 필요로 하지만, 거의 대부분의 경우 이런 복잡함이 요구되지 않는다.
- 메시지 하나를 보내는 것보다 호출이 조금 더 구체적이고 또 조작하기 쉬워지려면, 객체가 해답이 된다.
- 호출 자체를 나타내기 위한 객체를 만드는 것이다. 객체를 생성할 때 계산에 필요한 모든 매개 변수들을 초기화하고, 호출할 준비가 되면 `run()` 과 같은 프로토콜을 이용해서 계산을 호출한다.

```java
// 자바의 Runnable 인터페이스는 훌륭한 예다.
interface Runnable
		public abstract void run();
```



## 값 객체

> 객체가 생성된 이후 그 값이 절대로 변하지 않게 하여 별칭 문제가 발생하지 않게 한다.

- 널리 공유해야 하지만 동일성(identity)은 중요하지 않을 때는 객체가 생성될 때 상태를 설정한 후 이 상태가 절대 변할 수 없도록 한다.
- 그리고 이 객체에 대한 수행되는 연산은 언제나 새로운 객체를 반환하게 만든다.

### 별칭문제

- 두 객체가 제 3의 다른 객체에 대한 참조를 공유하고 있는 상태라고 하자.
- 한 객체가 공유되는 객체의 상태를 변화시키면 다른 객체는 그 사실을 알 방법이 전혀 없다.
- 별칭 문제를 해결하기 위핸 몇 가지 방법
  1. 현재 의존하는 객체에 대한 참조를 결코 외부에 알리지 않는 방법
     - 대신 객체에 대한 복사본을 제공한다.
     - 하지만 수행 시간이나 메모리 공간 측면에서 비싼 해결책일 수도 있고, 공유 객체의 상태 변화를 공유하고 싶을 경우에는 사용할 수 없다는 단점이 있다.
  2. 옵저버 패턴 사용
     - 의존하는 객체에 자기를 등록해 놓고, 객체의 상태가 변하면 통지를 하는 방법
     - 옵저버 패턴은 제어 흐름을 이해하기 어렵게 만들 수 있고, 의존성을 설정하고 제거하기 위한 로직이 지저분해질 수 있다.
  3. **객체를 덜 객체답게 취급하기**
     - 객체를 변화 자체가 불가능하게 만들고, 참조를 원하는 곳 어디로든 넘겨준다.
     - ex. 정수 연산의 결과는 기존의 객체가 아니라 새로운 객체이다.
     - 객체 할당은 성능 문제를 야기할 수 있는데, 이런 문제는 모든 성능 문제와 동일하게 실질적인 자료 집합이 있고, 실질적 사용 패턴, 프로파일링 데이터, 성능에 대한 불만 등이 실재로 존재하는 상황 하에서만 고민해야 한다.

- 모든 값 객체는 동등성을 구현해야 한다.
  - 동일성(identity)과 동등성(equality)은 서로 다르다.
  - 5백원 동전 두 개가 서로 동등할지라도 동일하지는 않다.



## 널 객체

> 계산 작업의 기본 사례를 객체로 표현한다.

- 객체의 특별한 상황을 표현하고자 할 때 그 상황을 표현하는 새로운 객체를 만든다.
- 그리고 이 객체에 대한 다른 정상적인 상황을 나타내는 객체와 동일한 프로토콜을 제공한다.



### 예시

- 기존 - null을 확인하는 if문을 작성한다.

```java
public boolean setReadOnly() {
  		SecurityManager guard = System.getSecurityManager();
  		if (guard != null) {
        		guard.canWrite(path);
      }
  		return fileSystem.setReadOnly(this);
}
```



- 널 객체 사용 - null 상태를 표현하는 새로운 널 객체 `LaxSecurity`를 만든다.

```java
public boolean setReadOnly() {
  		SecurityManager guard = System.getSecurityManager();
      guard.canWrite(path);
  		return fileSystem.setReadOnly(this);
}

// LaxSecurity
public void canWrite(String path){}

// SecurityManager
public static SecurityManager getSecurityManager() {
  		return security == null ? new LaxSecurity() : security;
}
```





## 템플릿 메서드

> 계산 작업의 변하지 않는 순서를 여러 추상 메서드로 표현한다. 이 추상 메서드들은 상속을 통해 특별한 작업을 수행하게끔 구체화된다.

- 작업 순서는 변하지 않지만 각 작업 단위에 대한 미래의 개선 가능성을 열어두고 싶은 경우
  - 다른 메서드들을 호출하는 내용으로만 이루어진 메서드를 만든다.
- 상위클래스에는 다른 메서드를 호출하는 내용으로만 이루어진 메서드를 만들고
- 하위클래스에서는 이 각각의 패턴을 서로 다른 방식으로 구현한다.

<img src="./images/chapter 30-1.png" alt="chapter 30-1" style="zoom:33%;" />

## 플러거블 객체

> 둘 이상의 구현을 객체를 호출함으로써 다향성을 표현한다.

- 변이를 표현하는 가장 간단한 방법은 명시적인 조건문을 사용하는 것이다.
- 하지만 이러한 명시적인 의사 결정 코드는 여러 곳으로 펴져나간다.

```java
if (circle) {...}
else {...}
```



### 예시

- 중복 조건문들이 존재한다.

```java
Figure selected;
public void mouseDown() {
  		selected = FindFigure();
  		if (selected != null)
        	select(selected);
}

public void mouseMove() {
  		if (selected != null)
        	move(selected);
  		else
        	moveSelectionRectangle();
}

public void mouseUp() {
  		if (selected == null)
        	selectAll();
}
```



- 플러거블 객체인 `SelectionMode`를 만들고 이를 구현하는 `SingleSelection`과 `MultipleSelection`을 만든다.

```java
SelectionMode mode;
public void mouseDown() {
  		selected = FindFigure();
  		if (selected != null)
        	mode = SingleSelection(selected);
  		else
        	mode = MultipleSelection();
}

public void mouseMove() {
  		mode.mouseMove();
}

public void mouseUp() {
			mode.mouseUp();
}
```



## 플러거블 셀렉터

> 객체별로 서로 다른 메서드가 동적으로 호출되게함으로써 필요 없는 하위 클래스의 생성을 피한다.

- 인스턴스별로 서로 다른 메서드가 동적으로 호출되게 하려면, 메서드의 이름을 저장하고 있다가 그 이름에 해당하는 메서드를 동적으로 호출한다.

### 예시

1. 상속 이용하기 : 상속은 작은 변이를 다루기에는 무거운 기법이다.

```java
abstract class Report {
		abstract void print();
}
class HTMLReport extends Report {
  	void print() {...}
}
class XMLReport extends Report {
  	void print() {...}
}
```



2. switch문 이용하기 : 새로운 종류의 출력을 추가할 때마다 기존 코드를 수정해야 한다.

```java
abstract class Report {
		String printMessage;
  	Report(String printMessage) {
      		this.printMessage = printMessage;
    }
  	void print() {
      		switch (printMessage) {
            case "printHTML" :
              	printHTML();
              	break;
            case "printXML" :
              	printXML();
              	break;
          }
    }
  	void printHTML(){...}
    void printXML(){...}
}
```



3. 플러거블 셀렉터 해법 : 리플랙션을 이용하여 동적으로 메서드를 호출한다.

```java
void print() {
		Method runMethod = getClass().getMethod(printMessage, null);
		runMethod.invoke(this, new Class[0]);
}
```



## 팩토리 메서드

> 생성자 대신 메서드를 호출함으로써 객체를 생성한다.

- 새 객체를 만들 때 생성자를 사용하는 경우 분명히 객체 하나를 생성하고 있다는 것을 알 수 있다.
  - 그러나 생성자는 표현력과 유연함이 떨어진다.
- 우리가 필요로 하는 유연함은 생성자에서 다른 클래스의 객체를 생성할 수 있게 하는 것이다.
- 메서드라는 한 단계의 인디렉션을 추가함으로써 다른 클래스의 인스턴스를 반환할 수 있는 유연함을 얻을 수 있다.

```java
// Money.class
static Dollar dollar(int amount) {
		return new Dollar(amount);
}
```



## 사칭 사기꾼

> 현존하는 프로토콜을 갖는 다른 구현을 추가하여 시스템에 변이를 도입한다.

- 기존 코드에 새로운 변이를 도입하려면, 기존의 객체와 같은 프로토콜은 갖지만 구현은 다른 새로운 객체를 추가한다.(다형성)
- 일반적으로 사칭 사기꾼을 사용할 곳을 한번에 집어내는 데에는 통찰력이 필요하다.
- 리팩토링 중에 나타나는 사칭 사기꾼의 두 가지 예시
  - 널 객체 - 데이터가 없는 상태를 데이터가 있는 상태와 동일하게 취급할 수 있다.
  - 컴포지트 - 객체의 집합을 단일 객체처럼 취급할 수 있다.

### 예시

- 이미 사각형(rectangle)을 제대로 그리는 상황이라면, 사각형 대신 타원(OvalFigure)을 넣으면 된다.

```java
testRectangle() {
  	Drawing d = new Drawing();
  	d.addFigure(new RectangleFigure(0, 10, 50, 100));
  	RecordingMedium brush = new RecordingMedium();
  	d.display(brush);
  	assertEquals("rectangle 0 10 50 100\n", brush.log());
}

testOval() {
  	Drawing d = new Drawing();
  	d.addFigure(new OvalFigure(0, 10, 50, 100));
  	RecordingMedium brush = new RecordingMedium();
  	d.display(brush);
  	assertEquals("oval 0 10 50 100\n", brush.log());
}
```



## 컴포지트

> 하나의 객체로 여러 객체의 행위 조합을 표현한다.

- 하나의 객체가 다른 객체 목록의 행위를 조합한 것처럼 행동하게 만들려면, 객체 집합을 나타내는 객체를 단일 객체에 대한 임포스터로 구현하면 된다.

### 예시

- Transaction은 값의 증분을 저장한다
- Account는 Transaction들의 합을 계산함으로써 잔액을 얻어낸다.

```java
public Transaction {
		Money value;
		Transaction(Money value) {
			this.value = value;
		}
}

public Account {
    Transaction transactions[];
    Money balance() {
        Money sum = Money.zero();
        for (int i = 0; i < transactions.length; i++)
            sum = sum.plus(transactions[i].value);
        return sum;
    }
}
```



- 고객은 여러 계좌를 가지고 있고 전체 계좌의 잔액을 알고 싶어한다.
- Account와 Balance가 동일한 인터페이스(`Holding`)를 갖게 만들자

```java
interface Holding {
  	Money balance();
}

public Transaction implement Holding {
    Money value;
    Transaction(Money value) {
        this.value = value;
    }
    Money balance() {
        return value;
    }
}

public Account implement Holding {
    Holding holdings[];
    Money balance() {
        Money sum = Money.zero();
        for (int i = 0; i < holdings.length; i++)
            sum = sum.plus(holdings[i].balance());
        return sum;
    }
}
```

- 위의 예시는 컴포넌트의 냄새가 드러나 있다.
  - 실세계에서는 거래(transaction)에 잔액(balance)이 존재하지 않는다.
- 컴포지트 패턴을 적용하는 것은 프로그래머의 트릭이지, 세상 사람들에게 일반적으로 받아들여지는 것은 아니다.



## 수집 매개 변수

> 여러 다른 객체에서 계산한 결과를 모으기 위해 매개 변수를 여러 곳으로 전달한다.

- 여러 객체에 걸쳐 존재한는 오퍼레이션의 결과를 수집하려면, 결과가 수집될 객체를 각 오퍼레이션의 매개변수로 추가한다.

### 예시

- 결과가 수집될 `ObjectOutput` 객체를 매개변수로 받아서 처리한다.

```java
public interface Externalizable extends java.io.Serializable{
		void writeExternal(ObjectOutput out) throws IOException;
}
```



## 싱글톤

- 전역 변수를 제공하지 않는 언어에서는 전역 변수를 사용하지 마라
