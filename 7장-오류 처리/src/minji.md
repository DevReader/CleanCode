# 1️⃣ Flutter 판매 관련 애플리케이션
```dart
/* 개선 전 */
Future<List<Menu>> getMenus() async {
    final prefs = await SharedPreferences.getInstance();
    final res = await _api.req("URL", HttpMethod.get,
        type: UrlType.dev, needToken: true);
    if (res.statusCode == 200) {
      return (jsonDecode(res.body)["data"] as List)
          .map((e) => Menu.fromJson(e))
          .toList();
    } else {
      throw Exception("http Exception");
    }
}
```

## 문제점
- 예외에 의미를 제공해라 🆘 예외에 의미가 담겨있지 않아 파악하기 어려움

## 좋았던점
- 미확인 예외를 사용하라 ✅ 예외를 statusCode 별로 분리하지 않고 Exception 하나로 처리함

<br/>

# 개선
```dart
/* 개선 후 */
Future<List<Menu>> getMenus() async {
    final prefs = await SharedPreferences.getInstance();
    final res = await _api.req("URL", HttpMethod.get,
        type: UrlType.dev, needToken: true);
    if (res.statusCode == 200) {
      return (jsonDecode(res.body)["data"] as List)
          .map((e) => Menu.fromJson(e))
          .toList();
    } else {
      throw Exception("[${res.statusCode}]${jsonDecode(res.body)["message"]}");
    }
}
```

## 🥔 Exception에 statusCode 와 에러 메세지 넣기
- 기존에 디버깅툴로 확인했던 statusCode 와 에러 메세지를 보다 편하게 확인할 수 있게 변경함

<br/>
<br/>

# 2️⃣ Flutter 판매 관련 애플리케이션
```dart
/* 개선 전 */
Future<void> pickImage() async {
    final picker = ImagePicker();
    final pickedImg = await picker.pickImage(source: ImageSource.gallery);
    try {
      if (pickedImg != null) {
        updateImgUrl(imgUrl);
      } else {
        showToast("이미지를 가져오는데 실패했습니다.");
      }
    } catch (e) {
      throw Exception("이미지를 가져오는데 실패했습니다.");
    }
    notifyListeners();
  }

void updateImgUrl(String? imgUrl) {
  _imgUrl = imgUrl;
  notifyListeners();
}
```

## 문제점
- null 을 반환하지 마라 🆘 pickedImg 에 null 을 확인하는 코드를 넣음
- null 을 전달하지 마라 🆘 updateImgUrl 에 인자로 null 이 들어갈 수 있게 함

## 좋았던점
- Try-Catch-Finally 문부터 작성하라 ✅ try-catch 문부터 작성함

<br/>

# 개선
```dart
/* 개선 후 */
FFuture<void> pickImage() async {
  final picker = ImagePicker();
  final pickedImg = await picker.pickImage(source: ImageSource.gallery);
  try {
    updateImgUrl(imgUrl);
  } catch (e) {
    showToast("이미지를 가져오는데 실패했습니다.");
    throw Exception("이미지를 가져오는데 실패했습니다.");
  }
  notifyListeners();
}

void updateImgUrl(String imgUrl) {
  _imgUrl = imgUrl;
  notifyListeners();
}
```

## 🥔 updateImgUrl 의 인자를 not null 로 변경
not null 로 변경 한 후 _imgUrl 을 null 로 초기화 하는 별도의 함수를 작성했다.

## 🥔 picked 이미지가 null인지 확인하는 부분 삭제
null 인지 확인하는 조건문 대신 try-catch 를 활용했다.

<br/>
<br/>

# 생각해볼 점
1. nullable 한 변수를 많이 사용하다보니 null 을 인자로 받고, 조건문을 사용한 부분이 많았다. 과연 이 변수가 정말 nullable 할 이유가 있는지 다시 한 번 확인해보자.
2. API 통신 하는 부분도 try-catch 활용해서 개선하면 좋을 것 같다.