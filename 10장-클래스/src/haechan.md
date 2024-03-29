### 정리
**클래스는 작게 만든다.**<br/>
- 단일 책임 원칙(SRP)에 따라 분리한다.<br/>
- 클래스의 이름에 책임을 기술한다.<br/>
- 응집도<sup>1</sup>를 높인다.<br/><br/>

**변경 가능성을 고려한다.**<br/>
- 개방 폐쇄 원칙(OCP)<sup>2</sup>을 준수한다.<br/>
- ``인터페이스``와 ``추상 클래스``를 활용한다.<br/>
- ``위임``을 활용한다.<br/><br/>

### 실습
**[기존 코드]**<br/>
```kotlin
// 뷰의 요구 사항을 담당하는 함수가 하나의 파일에 전역 함수로 설정되어 있다.
fun calcItemHeight(itemSize: Dp, degree: Double) { ... }
fun getRotationDegree(layoutInfo: LazyListLayoutInfo, indexInVisibleItems: Int): Double { ... }
```

<br/>

➡️ 관련성 있는 요구 사항끼리 묶어 클래스로 분리하기.<br/><br/>

❓ 하나의 파일 안에 둘까, 다른 클래스로 분리할까?<br/>
- 뷰의 요구 사항이 다양한 상황. Ex. 폴링 동작, 오프셋에 따른 각도 측정, 높이 변화 등.<br/>
- 현재 파일 길이는 273줄.<br/>
- [이 글](https://medium.com/mj-studio/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%9D%B4%EB%A0%87%EA%B2%8C-%EC%9E%91%EC%84%B1%ED%95%98%EC%8B%9C%EB%A9%B4-%EB%90%A9%EB%8B%88%EB%8B%A4-94871a1fa646)에서는 전역 함수로 두는 걸 추천하고 있다.<br/><br/>

<sup>1</sup>응집도(Cohesion): 모듈 내부 요소 간의 의존성.<br/>
<sup>2</sup>개방 폐쇄 원칙: 확장에 대해서는 개방적(Open)이고, 수정에 대해서는 폐쇄적(Closed)이어야 한다.<br/>
