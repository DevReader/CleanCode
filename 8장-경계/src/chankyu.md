# 8장 경계

  

```js

const [userMarker, setUserMarker] = useState<kakao.maps.Marker>();

const [dogFootMarker, setDogFootMarker] = useState<kakao.maps.Marker>();

```

  

## 외부 객체 사용

- 외부 객체를 중간 인터페이스 없이 그대로 사용하였다

- 실제로도 naver -> kakao로 외부 소스를 변경했었는데 그럴 때마다 컴포넌트 코드도 전부 변경해야 했다

- CustomMap 객체로 경계 클래스를 래핑해서 불필요한 기능을 제한하고 내부 로직에 알맞게 사용하면 좋을 것 같다

  

## 학습 테스트에 대한 생각

- 외부 코드에 대해 테스트를 짜는 것이 과연 맞을까?

- 일반적인 상황에선 외부 코드는 잘 작동한다고 생각하고 짜는게 맞는 것 같다

- 외부 코드에 대해서 공식문서에 나온 것 보다 더 깊이 이해하고 활용하고 싶을 때, 동작 위주로 테스트하면 괜찮을 것 같다