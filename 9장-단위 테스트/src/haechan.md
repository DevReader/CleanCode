### 정리
**TDD 법칙 세 가지**<br/>
1. 실패하는 단위 테스트를 먼저 작성한다.<br/>
2. 컴파일만 통과하는 테스트를 작성한다.<br/>
3. 테스트만 통과하는 테스트를 작성한다.<br/><br/>

**가독성**<br/>
- Build-Operate-Check 패턴 사용하기.<br/>
- 인터페이스 제공하기.<br/>
- 테스트 환경과 실제 환경 구분하기(최적화 필요 없음).<br/><br/>

**개념 당 assert 하나**<br/>
- JUnit @Tag 사용하기.<br/><br/>

### 실습
**[기존 코드]**<br/>
```kotlin
// 비슷한 기능의 테스트가 그룹화되어 있지 않다.
@Test
fun supportsNumberWithAddition() {
    assertEquals(toDecimal("MMVI"), 2006)
}

@Test
fun supportsNumberWithSubtraction() {
    assertEquals(toDecimal("MCMXLIV"), 1944)
}

```

<br/>

➡️ 그룹화하고 이름 붙이기("숫자 연산을 지원한다" 등)<br/>
