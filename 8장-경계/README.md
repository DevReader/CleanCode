# 8장 경계
> 어떤 식으로든 이 외부 코드를 우리 코드에 깔끔하게 통합해야만 한다.<br/>
> \- 144p -

## 외부 코드 사용하기
- 경계 인터페이스를 새로 정의한 클래스 내에 캡슐화하면 필요한 인터페이스만 사용해 외부 코드가 설계 규칙과 비즈니스 규칙을 따르도록 강제할 수 있고 경계 인터페이스가 변하더라도 나머지 프로그램에는 영향을 미치지 않게 할 수 있다.
- 모든 경계 인터페이스를 캡슐화할 필요는 없지만 경계 인터페이스를 여기저기 넘기지 말아야 한다.

## 경계 살피고 익히기
- 외부 코드를 도입하기 전에 간단한 테스트 케이스를 작성해 외부 코드를 익히는, 학습 테스트를 진행해보자.
- 학습 테스트를 통해 API 를 목적에 맞게 사용하고 제대로 이해할 수 있다.

## 학습 테스트는 공짜 이상이다
- 학습 테스트엔 드는 비용이 없다.
- 학습 테스트를 이용한 학습이 필요 없더라도 실제 코드와 동일한 방식으로 인터페이스를 사용하는 테스트 케이스가 필요하다.

## 아직 존재하지 않는 코드를 사용하기
1. 자체적으로 인터페이스 정의하기
2. 정의한 대로 인터페이스 구현하기
3. 존재하지 않는 코드가 정의된 후에 Adpater를 구현해 간극 채우기

## 깨끗한 경계
- 경계에서는 다양한 변경이 이루어지므로 너무 많은 투자를 하거나 향후 변경 비용이 지나치게 커지지 않도록 각별히 유의해야 한다.
- 경계에 위치하는 코드는 깔끔히 분리한다.
- 기대치를 정의하는 테스트 케이스를 작성한다.
- 외부 패키지를 호출하는 코드를 가능한 줄인다.
