## 아이템 34 - int 상수 대신 열거 타입을 사용하라

- 자바 초기에는 열거 개념이 없어서 정수 상수로 상태나 타입을 표현했다

```java
public static final int APPLE_FUJI = 0;
public static final int APPLE_PIPPIN = 1;
public static final int APPLE_GRANNY_SMITH = 2;
```

- 이렇게 하면 단점 :
  - 타입이 안전하지 않다 : 다른 상수를 잘못 넣어도 컴파일러가 못 잡음
  - 디버깅 불편하다 -> 왜냐하면 출력한다고 했을때 단순 숫자만 나옴
  - 확장성이 낮다

<br/>
 
**열거 타입 사용**
```java
public enum Apple { FUJI, PIPPIN, GRANNY_SMITH }
public enum Orange { NAVEL, TEMPLE, BLOOD }
```

- 장점 :
  - 타입 안정성
  - 디버깅할때 가독성이 좋아진다
  - 메서드, 필드, 생성자 등을 추가할 수 있어서 기능 확장이 좋아진다
  - 싱글턴 보장으로 각 상수는 하나의 인스턴스만 존재하도록 보장한다 

<br/>

**전략 열거 타입 패턴**

- 보통 enum은 단순하게 값 만 담는 용도로 쓰인다
- 하지만 각 상수가 다른 알고리즘이나 동작을 가져야 하는 상황이 있다
- 그래서 각 상수에서 메서드를 오버라이딩하여 서로 다른 동작을 정의한다
- 데이터와 함께 사용할수 있다

- 장점
  - 전략을 enum으로 강제해서 잘못된 전략 사용이 불가능하다
  - 전략과 데이터를 한곳으로 묶을수 있어 응집도가 올라간다
  - 새로운 전략을 enum 상수 추가로 쉽게 확장할 수 있다
