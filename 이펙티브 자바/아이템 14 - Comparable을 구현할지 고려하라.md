## 아이템 14 - Comparable을 구현할지 고려하라
- 순서를 고려해야 하는 값 클래스를 작성한다면 꼭 Comparable 인터페이스를 구현해서
- 그 인스턴스들을 쉽게 정렬하고 검색하고 비교 기능을 제공하는 컬렉션과 어우러지도록 해야 한다

**compareTo 규약**
- 거의 equals()랑 같다고 생각하면 된다
- x.compareTo(y) 의 결과는 음수, 0, 양수 이고 의미가
  - 음수 -> x < y
  - 0 -> x == y
  - 양수 -> x > y
 
1. 대칭성
    - a.compareTo(b) > 0 이면 b.compareTo(a) < 0 이어야 함
2. 추이성
  - x > y 이고 y > z 이면 무조건 x > z
3. 일관성
  - x.compareTo(y) == 0 이면 x.equals(y) 도 true여야 함


<br/>

**기본 구현**
```java
public class Person implements Comparable<Person> {
    private String name;
    private int age;

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age);
    }
}
```
- 나이를 기준으로 오름 차순 정렬이 된다
- Comparable를 사용할때는 compareTo 메서드에서 값을 비교할때 < , > 연산자는 쓰지 말아야 한다
- 박싱된 기본 타입 클래스가 제공하는 정적 compare 메서드나 Comparator 인터페이스가 제공하는 비교자 생성 메서드를 사용하면 된다

<br/>

**compareTo 와 equals() 관계**
- compareTo() 결과가 0 이라면 equals() 도 true 가 되도록 구현해야한다
- 하지만 BigDecimal 같은 예외도 있다

<br/>

**Comparable, Comparator**

Comparable
- 클래스가 Comparable<T> 인터페이스를 직접 구현해야 하고 compareTo() 메서드를 구현한다
- 클래스 내부에서 순서를 정의할때 사용한다

Comparator
- 외부에서 정렬 기준을 지정할 때 사용한다
- 상황에 따라 정렬 기준이 달라진다면 활용하면 좋다
- 여러 기준이 필요할때 유용하다
- Comparator<T> 인터페이스를 별도로 구현하거나 람다식을 사용한다
