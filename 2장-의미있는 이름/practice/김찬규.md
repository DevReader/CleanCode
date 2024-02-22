## 실습
- 예전에 진행했던 프로젝트 중, massive한 hook에서의 state 선언문들을 가져왔습니다.
- 2장까지 읽은 내용을 바탕으로 아래 state들의 이름을 바꿔봅니다.
```js
/** Local State */
  const [map, setMap] = useState<kakao.maps.Map>();
  const [isAlertOpen, setIsAlertOpen] = useState(false);
  const [isSearchViewOpen, setIsSearchViewOpen] = useState(false);
  const [isSelectedAnything, setIsSelectedAnything] = useState(false);
  const [currentUserLocation, setCurrentUserLocation] = useState({ lat: 0, lng: 0 });
  const [dogFootMarkerLocation, setDogFootMarkerLocation] = useState({ lat: 0, lng: 0 });
  const [selectedMungple, setSelectedMungple] =
    useState<SelectedMungple>(defaultSelectedMungple);
  const [selectedCert, setSelectedCert] = useState<Cert>(certDefault);
  const [selectedCategory, setSelectedCategory] = useState('');
  const [isFirstRendering, setIsFirstRendering] = useState({ mungple: true, cert: true });
  const [isCertToggleOn, setIsCertToggleOn] = useState(initialCertMungpleToggle);
  // Markers
  const [userMarker, setUserMarker] = useState<kakao.maps.Marker>();
  const [dogFootMarker, setDogFootMarker] = useState<kakao.maps.Marker>();
  const [mungpleMarkers, setMungpleMarkers] = useState<MungpleMarkerType[]>([]);
  const [certMarkers, setCertMarkers] = useState<kakao.maps.CustomOverlay[]>([]);
  const [mungpleCertMarkers, setMungpleCertMarkers] = useState<
    kakao.maps.CustomOverlay[]
  >([]);
  const [cluster, setCluster] = useState<kakao.maps.MarkerClusterer>();
```

### map -> globalMap
- 가장 넓은 범위에서 사용하는 변수인데 검색하기 어려운 상태
### currentUserLocation -> userMarkerCoords
- current라는 불필요한 맥락 제거(유저 마커의 위치는 항상 current)
- Marker의 위치임을 알려주는 맥락 추가
- 좌표와 관련됨을 더 명확히 하기 위해 Location 대신 Coords사용
### dogFootMarkerLocation -> dogMarkerCoords
- Marker의 위치임을 알려주는 맥락 추가
- 좌표와 관련됨을 더 명확히 하기 위해 Location 대신 Coords사용
### selectedMungple -> selectedPlace
- 프로젝트 외부인이 이해하기 어려운 이름을 변경
### selectedCert -> selectedCertification
- 인코딩 제거 Cert -> Certification
### isFirstRendering -> initialRenders
- 초기 상태라는 정보를 initial 접두사로 명확히 함
- 객체 형태이기 때문에 boolean값 변수 앞에 is가 붙는 일관성을 억지로 고려하지 않아도 됨

## '한 개념에 한 단어를 사용하라'에 대한 추가 탐구
실제로 개발을 하다보면 한 개념에 한 단어를 일관성 있게 쓰는법이 어렵다는 사실을 느낀다. 이전에 내가 썼던 단어가 get인지 fetch인지 헷갈리고, 남이 같은 개념을 어떻게 작성했었는지 알기 어렵다. 위 개념이 좋다는 사실은 누구나 알고 있지만 그럼 어떻게 지킬 수 있는걸까?

### 프로젝트 전체에 대한 용어집 작성
프로젝트의 주요 개념, 함수, 컴포넌트 등에 사용되는 용어에 대한 용어집을 작성하면 프로젝트에 참여하는 모든 개발자가 동일한 용어를 사용할 수 있다. 중간에 새로 들어온 사람이 생기면 용어집에서 검색하면된다. 물론 용어집을 만드는게 쉬운일은 아니다. 

### 같이 ERD 데이터 타입 정의하기
프로젝트에서 가장 메인으로 다루는 도메인에 관련된 변수나 객체에 대해서는 개발자들이 다 같이 이름을 정하는 것이 좋다.

### 코드 리뷰 문화 정착
한번에 완벽한 코드를 만들 수 없다. 코드는 계속 보살피고 더 좋은 코드로 개선하는 과정을 반복해야 좋아진다. 코드 리뷰를 통해 본인과 동료들의 코드에서 사용된 용어들이 일관적인지, 프로젝트 용어집과 일치하는지 확인할 수 있다.