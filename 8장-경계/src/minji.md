# 1️⃣ Flutter 판매 관련 애플리케이션
```dart
LatLng(
  double.parse(json['detail']['lat']),
  double.parse(json['detail']['lon']),
),
```

## 문제점
* 구글 맵에서 사용하는 LatLng 클래스를 앱 전체에서 사용하고 있다.
* 추후 구글 맵이 아닌 네이버, 카카오맵으로의 변경이 어려울 수 있다.

<br/>

## 개선
* LatLng 을 전역에서 사용하는 대신 위치와 관련된 클래스를 새로 정의해서 진행한다.