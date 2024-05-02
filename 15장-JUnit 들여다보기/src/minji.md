# 정리
## JUnit 프레임워크
### ComparisonCompactor 변경점
- 캡슐화 되지 않은 조건문 캡슐화
- 이름을 명확하게 변경
  - 변수명에 index 추가
  - 길이를 의미하는 변수에 index -> length 로 변경
  - 조건문에 의해 false 일 경우 compact 하지 않기 때문에 함수명 compact -> formatComapctedComparison 으로 변경
- 부정문은 긍정문보다 이해하기 어려우므로, 부정문인 조건문을 긍정문으로 변경
- 수행하는 내용이 더 정확하게 나타나도록 함수명 변경
- 곳곳에 등장하는 +1 삭제

### 결론
- 코드를 리팩터링 하다 보면 원래 했던 변경을 되돌리기도 함