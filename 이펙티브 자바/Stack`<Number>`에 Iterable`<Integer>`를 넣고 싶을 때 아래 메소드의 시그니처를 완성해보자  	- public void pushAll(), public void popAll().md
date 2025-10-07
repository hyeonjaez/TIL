## Stack`<Number>`에 Iterable`<Integer>`를 넣고 싶을 때 아래 메소드의 시그니처를 완성해보자  	- public void pushAll(), public void popAll()

- Stack<Number> 가 있다
- 여기에 Iterable<Integer> 원소들을 모두 push 하고 싶다고 하자 -> 하위 타입의 요소들을 상위 타입 스택에 넣음 
- 반대로 스택에서 꺼낸 요소들을 Collection<Object>에 모두 pop하고 싶다고 하자 -> 상위 타입 컬렉션에 하위 타입 요소들을 넣음

**와일드 카드의 PECS 원칙**
- Producer-Extends, Consumer-Super
- 데이터를 생산(Produce) 하는쪽에는 extends 사용
- 데이터를 소비(Consume) 하는 쪽에는 super 사용


```java
public class Stack<E> {

  private List<E> elements = new ArrayList<>();

  public void pushAll(Iterable<? extends E> it){
    for(E e : it) {
      push(e);
    }
  }

  public void popAll(Collection<? super E) coll){
    while(!elements.isEmpty()){
      coll.add(pop());
    }
  }

}
```

<br/>

**나의 정리**

- 상위 타입에 쓸때는 super
- 하위 타입 데이터를 읽을때는 extends







