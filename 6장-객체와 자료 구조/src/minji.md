# 1️⃣ Flutter 판매 관련 애플리케이션
```dart
/* 개선 전 */
...
  await SharedPreferences.getInstance().then((value) {
    value.setBool("visited", true);
  })
```

## 문제점
1. 디미터 법칙 - 기차 충돌 🆘 getInstance 메서드가 반환하는 SharedPreferences 객체의 메서드를 또 호출함
  <br/> 매번 SharedPreference 객체를 나누어 작성하는 것이 지저분하다고 생각해서 위와 같이 작성했었음.

# 개선
```dart
/* 개선 후 */
...
  final SharedPreferences prefs = await SharedPreferences.getInstance();
  prefs.setBool("visited", true);
```

## 🥔 기차 충돌을 방지하도록 코드 분리
* 인스턴스를 담는 prefs 를 선언하고 prefs 에서 메서드를 호출하도록 코드를 분리.
