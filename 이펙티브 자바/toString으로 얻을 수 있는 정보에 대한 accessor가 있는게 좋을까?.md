##  toString으로 얻을 수 있는 정보에 대한 accessor가 있는게 좋을까?

### 🧠 개념 설명
- toString()은 주로 디버깅, 로깅 에서 보기 쉽게 하기위함
- 사람이 읽기 좋은 문자열 표현을 제공하는 것이다 

**Accessor 와의 관계**
- toString()에 담기는 정보가 도메인 로직에서 실제로 필요할땐 접근할 공식적인 accessor메서드를 제공하는 것이 맞다
- toString()만 두고 getter를 제공하지 않다면
  - 로깅, 출력에는 유용하지만 코드 레벨에서 필요한 값을 꺼내 쓸수 없다
  - 만약 꺼내 쓸려고 하면 toString()을 가지고 문자열 파싱 해야함
 
**toString()과 Accessor**
- toString은 사람이 읽을 수 있는 문자열 표현 용도로만 쓰인다
- 비즈니스 로직에 필요한 데이터는 반드시 accessor제공 한다
- 그래서 toString에 나오는 정보와 getter제공 여부는 관련되어 있지 않은 문제
- 필요한 값이라면 getter 제공, 단순하게 로그 용이라면 getter 필요 없음
