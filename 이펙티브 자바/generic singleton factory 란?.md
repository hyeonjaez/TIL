## generic singleton factory 란?

- 하나의 객체를 여러 타입으로 안전하게 재사용할 수 있도록 만든 제네릭 팩토리 메서드이다.
- 다시 말해서 실제 인스턴스는 하나지만 사용하는 시점마다 타입을 다르게 반환할수 있는 제네릭 메서드 구조이다.


<br/>

**왜 필요할까?**
```java
public static UnaryOperator<Object> IDENTITY_FN = (t) -> t;
```

- 이렇게 입력값을 그대로 반환하는 함수가 있다고 하자
- 그리고 위 코드에서 IDENTITY_FN 은 싱글턴 함수 객체이다.

```java
UnaryOperator<String> same = IDENTITY_FN; // 컴파일 경고 발생
```
- 이 객체는 UnaryOperator<Object> 타입이라 위 코드처럼 작성하면 타입 불일치가 생긴다

<br/>

**해결 방법은**
```java
private static UnaryOperator<Object> IDENTITY_FN = (t) -> t;

@SuppressWarnings("unchecked")
public static <T> UnaryOperator<T> identityFunction() {
    return (UnaryOperator<T>) IDENTITY_FN;
}
```
- 위 코드 처럼 제네릭 메서드를 하나 만들어서 타입 안전하게 꺼내 쓰는 방법이다.
- IDENTITY_FN 객체는 하나만 존재한다
- 제네릭 메서드 를 통해 타입을 바꿔서 안전하게 반환한다


<br/>

**나의 정리**
- 제네릭 싱글턴 팩터리는 하나의 객체를 여러 타입으로 안전하게 재사용할 수 있도록 하는것이다.
- 인스턴스는 하나지만 사용하는 시점에 따라서 타입을 다르게 반환하는 것이다.
