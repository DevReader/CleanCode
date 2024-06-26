## 11장 시스템
시스템 수준해서 깨끗함을 유지하는 방법.<br/><br/>

### 정리
**생성과 사용을 분리한다.**<br/>
- 생성과 사용을 같이 하면 단일 책임 원칙(SRP)에 위배되고, 테스트하기 어렵다.<br/>
- 생성을 main()으로 분리한다.<br/>
- Abstract Factory 패턴<sup>1</sup>을 적용한다.<br/>
- 의존성을 주입한다.<br/><br/>

**아키텍처는 작게 만들고 확장한다.**<br/>
- 관심사<sup>2</sup>를 분리한다.<br/>
- 프레임워크, 애너테이션 등을 사용한다.<br/><br/>

**도메인 특화 언어를 사용한다.**<br/><br/>


<sup>1</sup>Abstract Factory 패턴: 하나의 제품군을 생성하는 패턴.<br/>
<sup>2</sup>관심사: 프로그램이 해결하고자 하는 개별적인 기능이나 목적.<br/>
