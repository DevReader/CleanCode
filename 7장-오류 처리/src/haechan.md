## 7장 오류 처리
### 정리
__비즈니스 논리와 오류 처리를 뒤섞지 않는다__
- 특수 사례 패턴을 이용한다
- null을 전달하거나 반환하지 않는다<br/>
  (Nullable, NonNullable 구분하기)
- 오류코드보다 예외를 선호한다
<br/><br/>

__미확인 예외를 사용한다__
- 확인된 예외는 OCP를 위반한다
<br/><br/>

__예외는 처리 방법에 따라 분류한다__
- Try-Catch문에서 중복을 제거할 수 있다
<br/><br/>

__Try-Catch-Finally문부터 작성한다__
- 범위가 존재하므로 논리적 일관성을 유지하기 쉽다
  <br/><br/>

### 실습
__[기존 코드]__<br/>
```
if (problemToEdit != null) { ... }
```
➡️ 문제가 선택되지 않은 상태를 ``null`` 대신 ``EMPTY_PROBLEM`` 으로 표현
<br/>
