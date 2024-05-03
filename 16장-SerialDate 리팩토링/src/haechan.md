## 16장 SerialDate 리팩토링
### 코드 리뷰에 감사하기
- 코드 리뷰는 편안하게 여겨야할 활동이다.<br/>
- 남이 내게 해준다면 감사히 반겨야 할 활동이다.<br/><br/>

### 필요 없는 주석 없애기
- 필요한 주석: 라이선스 정보, 저작권 등.<br/>
- 불필요한 주석: 변경이력 등.<br/><br/>

### 명확한 이름 사용하기
- SerialDate라는 이름은 구현을 암시하지만 사실은 추상 클래스.<br/>
- SerialDate라는 이름은 날짜를 순서대로 표현한다는 의도를 잘 반영하지 못한다.<br/>
- SerialDate -> Date, DayDate, OrdinalDate<br/><br/>

### Enum 사용하기
- MonthConstants처럼 상수를 사용할때 static final을 쓰지 말고 enum을 쓰자.<br/>
- static final 변수를 interface에 모아 놓고 이를 구현하는 행동은 하지 말자.<br/><br/>

### 추상 클래스가 구현 클래스를 알게 하지 않기
- Abstract Factory 패턴을 사용하자.<br/>
- DayDateFactory처럼 Singletone 패턴과 함께 사용할 수 있다.<br/><br/>

### 불필요한 final 키워드 제거하기
- 실질적인 가치는 없으면서 코드만 복잡하게 만든다.<br/>
- 로버트 시몬스는 final 키워드 사용응 권장한다.<br/><br/>

