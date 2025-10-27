## IllegalStateException와 IllegalArgumentException

**IllegalStateException**
- 객체의 현재 상태가 메서드 호출을 처리하기에 적절하지 않을 때 발생시킨다
- 예를들어:
  - 아직 초기화되지 않은 객체에 메서드를 호출했을 때
  - 이미 닫힌 리소스에 다시 접근하려 할 때
- 값이 문제가 아니라 객체의 현재 상태가 메서드 실행에 적합하지 않기 때문에 발생한다

<br/>

**IllegalArgumentException**
- 메서드에 전달된 인자가 적절하지 않거나 유효하지 않을 때 발생 시킨다
- 호출자가 메서드 계약을 어겼을때
- null이나 범위를 벗어난 값을 전달했을 때
