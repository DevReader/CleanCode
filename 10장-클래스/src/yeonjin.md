### 클래스 체계

- 캡슐화
  변수와 유틸리티 함수는 가능한 공개하지 않는 편이 낫지만 반드시 숨겨야 한다는 법칙도 없다.

### 클래스는 작아야 한다.

클래스가 맡은 책임을 센다.

간결한 이름

클래스 설명: 만일, 그리고, 하며, 하지만을 사용하지 않고서 25단어 내외로 가능해야 함.

- 단일 책임 원칙
  클래스나 모듈을 변경할 이유가 하나뿐
- 응집도
  클래스는 인스턴스 변수 수가 작아야 한다.
  일반적으로 메서드가 변수를 더 많이 사용할수록 메서드와 클래스는 응집도가 더 높다.
  응집도가 높아지도록 변수와 메서드를 적절히 분리해 새로운 클래스 두세 개로 쪼개준다.
  응집도를 유지하면 작은 클래스 여럿이 나온다.

### 변경하기 쉬운 클래스

OCP 원칙: 클래스는 확장에 개방적이고 수정에 폐쇄적이어야 한다.

- 변경으로부터 격리
  DIP: 클래스가 상세한 구현이 아니라 추상화에 의존해야 한다는 원칙

### 궁금했던 점

- 개발 전 설계에 대한 경험을 물어보고 싶다
