## 아이템 58 - 전통적인 for 문보다는 for-each 문을 사용하라

**전통적인 for 문의 문제점**

```java
List<String> list = List.of("a", "b", "c");

// 전통적인 for 문
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// while + Iterator
for (Iterator<String> it = list.iterator(); it.hasNext();) {
    System.out.println(it.next());
}
```

- 인덱스 변수랑 반복자가 추가로 있다
- 컬렉션 수정 중 동기화 문제를 일으킨다.

<br/>

**for-each 문**
```java
for (String s : list) {
    System.out.println(s);
}
```
- 컬렉션이든 배열이든 동일하게 동작
- 인덱스나 반복자 관리 안해도 됨
- 코드가 간결하고 가독성 좋음

<br/>


**for-each 사용할수 없는 경우**
1. 파괴적인 필터링 : 선택된 원소를 제거해야할때

2. 변형 : 리스트나 배열을 순회하면서 그 원소의 값 일부나 전체를 교체해야할때

3. 병렬 반복 : 여러 컬렉션을 병렬로 순회해야 한다면 각각의 반복자와 인덱스 변수를 사용해서 제어해야 한다면



<br/>

**나의 정리**
- for-each 문은 명확하고 추가적인 반복자나 인덱스 변수를 사용하지 않아 버그를 예방해준다 성능저하도 없다
- Iterable을 구현한 객체라면 사용할수 있다 
