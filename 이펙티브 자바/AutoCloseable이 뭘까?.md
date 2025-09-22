## AutoCloseable이 뭘까?

### 🧠 개념 설명
- Java 7부터 도입된 인터페이스
- close() 메서드 하나만 정의되어 있다
- 목적 : 자원을 사용한 뒤 자동으로 해제할 수 있도록 보장하기 위함이다

<br/>

**언제 쓸까?**
- 파일, 소켓, 데이터베이스 커넥션 처럼 외부 자원을 다루는 객체는 사용후에 닫아야한다
- 과거에는 try-finally 구문으로 close()를 직접 호출해야 했다
- AutoCloseable를 구현하면 try-with-resources 구문을 통해서 자동으로 close 호출이 가능하다

<br/>

**AutoCloseable vs Closeable**
- 둘 다 자원 해제를 목적으로 사용하는 인터페이스
- Closeable은 java IO 전용으로 close() 가 IOException만 던진다
- AutoCloseable은 더 많은 곳에 쓰이고 close()가 Exception을 던질수 있다

---
### ✅ 한줄로 설명 하기
- 자원 사용후 close()를 자동으로 호출할 수 있도록 해주는 인터페이스이다 try-with-resources 문법을 가능하게 해준다
