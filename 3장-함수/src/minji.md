# 1️⃣ BOJ 3190번 뱀에 대한 풀이 코드

[문제 바로가기](https://www.acmicpc.net/problem/3190)

```python
# 개선 전
def isInRange(next):
    global N
    if next[0] < 0 or next[0] >= N or next[1] < 0 or next[1] >= N:
        return False
    return True
```

## 문제점

1. 단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야 한다. 🆘 인수명이 무엇을 의미하는지 잘 나타나 있지 않음
   <br/> next라는 인수명이 무엇을 의미하는지 알 수 없다.

<br/>

# 개선

```python
# 개선 후
def isInGameBoardRange(destinationIndexes):
    global N
    if destinationIndexes[0] < 0 or destinationIndexes[0] >= N or destinationIndexes[1] < 0 or destinationIndexes[1] >= N:
        return False
    return True
```

## 🥔 인수 및 함수명 변경

`isInRange` 👉 `isInGameBoardRange`
<br/>게임 판의 범위 임을 보다 명확하게 명시했다.

`next` 👉 `destinationIndexes`
<br/>목적지 index들을 담은 리스트임을 보다 명확하게 명시했다.

<br/>
<br/>

# 2️⃣ Flutter 판매 관련 애플리케이션, 지도 마커 관련 코드

```dart
Future<void> initMarkerIcon(String path, int width) async {
    final data = await rootBundle.load(path);
    final codec = await instantiateImageCodec(data.buffer.asUint8List(),
        targetWidth: width);
    final frameInfo = await codec.getNextFrame();

    _markerIcon = BitmapDescriptor.fromBytes(
      (await frameInfo.image.toByteData(format: ImageByteFormat.png))!
          .buffer
          .asUint8List(),
    );
  }
```

## 문제점

1. 한 가지만 해라 🆘 지도의 마커 아이콘을 초기화 하는 부분과 이미지를 변환하는 부분이 함께 쓰임
   <br/> 심지어 이미지를 바이트로 변환하는 함수는 다른 쪽과 중복된다.

2. 이항 함수 🆘 path와 width는 자연적인 순서가 있는 사항이 아님

<br/>

# 개선

```dart
/* 개선 후 */
Future<void> initMarkerIcon() async {
    await changeImgIntoBytesWithPathAndWidth("assets/imgs/img_30_marker_off.png", 90)
        .then((value) => _markerIcon = BitmapDescriptor.fromBytes(value));
  }

Future<Uint8List> changeImgIntoBytesWithPathAndWidth(String path, int width) async {
  final data = await rootBundle.load(path);
  final codec = await instantiateImageCodec(data.buffer.asUint8List(),
      targetWidth: width);
  final frameInfo = await codec.getNextFrame();
  return (await frameInfo.image.toByteData(format: ImageByteFormat.png))!
      .buffer
      .asUint8List();
}
```

## 🥔 함수 분리

`initMarkerIcon` 👉 `initMarkerIcon` & `changeImgIntoBytesWithPathAndWidth`
<br/>markerIcon 을 초기화 하는 부분과 Image 를 Byte 로 변환하는 부분으로 분리했다.

## 🥔 이항 함수명에 인수 키워드 사용

`initMarkerIcon` 👉 `changeImgIntoBytesWithPathAndWidth`
<br/>기존에 명시하지 않았던 인수명을 키워드로 함수에 명시함으로써 인수의 종류와 순서를 나타냈다.
