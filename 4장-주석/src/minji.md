# 1️⃣ Flutter 판매 관련 애플리케이션, 검색 API 코드

```dart
/* 개선 전 */
final res = await _api.req("/search?q=$keyword", HttpMethod.post,
    body: jsonEncode({
      "lat": latlng.latitude,
      "lon": latlng.longitude,
      "range": "100000000" // 수정 - range 협의
    }),
    type: UrlType.dev);
```

## 문제점
* 나쁜 주석 - 주절거리는 주석 🆘 어떤 협의가 필요하다는 것인지 명시가 되어있지 않음

## 좋았던점
* 좋은 주석 - TODO 주석 ✅ 미래에 변경이 필요한 부분에 대해 명시함

<br/>

# 개선
```dart
/* 개선 후 */
// TODO - range 값 변경 필요. 가게 더미 데이터 사용으로 인해 적절한 range를 측정할 수 없음. 실제 데이터 삽입 후 적절한 검색 범위를 백엔드와 협의해 range에 삽입
final res = await _api.req("/search?q=$keyword", HttpMethod.post,
    body: jsonEncode({
      "lat": latlng.latitude,
      "lon": latlng.longitude,
      "range": "100000000"
    }),
    type: UrlType.dev);
```

## 🥔 `수정` 👉 `TODO` 로 변경
* 주석의 용도가 명확하게 나타나는 태그 사용

## 🥔 구현하지 않은 이유 명시
* 기존에 변경 지점만 명시했다면 왜 현재 구현하지 못한 이유를 명확하게 표시해, 문제가 해결되었는지 더 쉽게 판단할 수 있도록 함
* 백엔드와 협의가 필요함을 명시함

## 🥔 미래 모습 설명
* range 에 대한 설명을 추가

<br/>
<br/>

# 2️⃣ Android 판매 관련 애플리케이션
```kotlin
/* 개선전 */
...
/*
        val selectedMartLiveData: LiveData<MartDataDTO> = sharedMartViewModel.getSelectedMart()

        selectedMartLiveData.observe(this) {
            it?.let { selectedMart ->
                updateUI(selectedMart)
            }
        }

         */
...
```

## 문제점
* 나쁜 주석 - 주석으로 처리한 코드 🆘 작동하지 않는 코드를 주석처리 해둠

# 개선
코드 삭제

## 🥔 코드 삭제
소스 코드 관리 시스템인 깃을 이용하고 있고, 이미 커밋 되어있는 내역이기에 해당 주석을 삭제했다.