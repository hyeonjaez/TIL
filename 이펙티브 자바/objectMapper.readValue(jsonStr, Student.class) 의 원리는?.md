## objectMapper.readValue(jsonStr, Student.class) 의 원리는?

1. Class<?> 타입 메타 데이터로부터 객체 생성

- Student.class는 타입 토큰 역할을 한다
- 이것으로 JSON 데이터를 어떤 타입으로 변환할지 결정한다
- 내부적으로 리플렉션을 사용해서 Student 클래스의 필드와 생성자를 조사한다.

<br/>

2. JSON 파싱
- jsonStr를 먼저 JSON 트리 구조로 파싱한다
- 이때 Jackson Streaming API, Tree Model 방식이 사용된다.


<br/>

3. 필드 이름 매핑
- Student 클래스의 필드와 JSON의 key를 매칭한다
- @JsonProperty 가 붙은 필드나 메서드
- 필드명과 JSON key가 동일한 경우에
- getter, setter 메서드가 존재하는 경우

<br/>

4. 인스턴스 생성
- 기본 생성자 호출
- Creator 메서드
- 만약 기본 생성자가 없다면 @JsonCreator를 붙인 생성자나 정적 팩토리 메서드를 사용한다

5. 값 주입
- 파싱된 JSON 값이 Student 필드에 주입된다
- 이때 Jackson은 내부적으로 Field.set()이나 Setter 메서드를 사용한다
- 타입 변환이 필요한 경우 Jackson의 Deserializer가 이것을 처리한다


<br/>

**이펙티브 자바 아이템 33 핵심**
```java
Favorites f = new Favorites();
f.putFavorite(String.class, "Java");
String s = f.getFavorite(String.class);
```
- String.class 가 타입 토큰 역할
- 런타임에도 String 타입 정보를 유지
- Class.cast()로 안전하게 캐스팅
- 타입 안전하게 다양한 타입의 객체를 저장, 조회할 수 있다

<br/>

**ObjectMapper.readValue 핵심**
```java
Student student = objectMapper.readValue(json, Student.class);
```
- Student.class 가 타입 토큰 역할
- Jackson이 런타임에 Student 타입 정보를 알고 있음
- 리플렉션으로 필드와 생성자를 탐색
- JSON을 Student 타입으로 안전하게 역직렬화
- 제네릭일 경우 TypeReference<T> 사용하여 런타임 타입 보존 가능

<br/>

**원리**
- ObjectMapper.readValue 메서드는 JSON 문자열을 자바 객체로 역직렬화 하는 기능으로
- 핵심은 Student.class 라는 타입 토큰을 전달받아 리플렉션을 통해 객체를 동적으로 생성하고 데이터를 주입한다
- 타입 정보를 런타임까지 보존하여 타입 안전하게 역직렬화를 수행하는 것이다.
