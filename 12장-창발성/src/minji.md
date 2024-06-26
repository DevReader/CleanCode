# 정리
## 창발적 설계로 깔끔한 코드를 구현하자
4가지 규칙을 지키면 다음과 같은 장점을 얻을 수있다.
- 코드 구조와 설계를 파악하기 쉬워진다.
- SRP 나 DIP 와 같은 원칙을 적용하기 쉬워진다.
- 우수한 설계의 창발성을 촉진한다.

## 단순한 설계 규칙 1 : 모든 테스트를 실행하라
- 설계는 의도한 대로 돌아가는 시스템을 내놓아야 한다.
- 테스트를 철저히 거쳐 모든 케이스를 항상 통과하는 시스템은 '테스트가 가능한 시스템'이다.
- 테스트가 가능한 시스템을 만들려고 하는 과정에서 설계 품질이 높아진다.

## 단순한 설계 규칙 2 ~ 4: 리팩터링
- 테스트 케이스를 모두 작성한 후 코드와 클래스를 점진저긍로 정리하라
- 테스트 케이스가 있기에 코드를 정리하며 시스템이 깨지지 않는다.

## 중복을 없애라
- 중복을 없애 새 메서드로 뽑고 클래스가 SRP를 위반한다면, 메서드를 다른 클래스로 이동시킨다. 이 과정에서 새 메서드의 가시성이 높아진다.
- 소규모 재사용은 시스템 복잡도를 극적으로 줄여준다.

## 표현하라
- 좋은 이름을 선택해라.
- 함수와 클래스 크기를 가능한 줄여라.
- 표준 명칭을 사용해라.
- 단위 테스트를 꼼꼼히 작성해라.
- 나중에 읽을 사람을 고려해 보다 읽기 쉽게 만드는 노력을 해라

## 클래스와 메서드 수를 최소로 줄여라
- 가능한 독단적인 견해는 멀리하고 실용적인 방식을 택해라
- 함수와 클래스를 작게 유지하면서 동시에 시스템 크기도 작게 유지해라
- 테스트 케이스를 만들고 중벅을 제거하고 의도를 표현하는 작업이 함수와 클래스를 만드는 작업보다 우선순위가 높다.