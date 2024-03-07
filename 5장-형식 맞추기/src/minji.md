# 1️⃣ Flutter 판매 관련 애플리케이션

```dart
/* 개선 전 */
class HomeViewModel with ChangeNotifier {
  late final HomeService _service;
  final AdminService _adminService = AdminService();

  bool _isLoading = true;
  List<Category>? _categories;
  List<Tab>? _tabs;
  List<StoreHome?> _maxDiscountStores = [];
  List<List<Menu>> _discountMenus = [];

  HomeViewModel(BuildContext context) {
    ...
  }

  Order _order = Order.values.first;

  Future<void> getMaxDiscountStores() async {
    ...
    _maxDiscountStores = [
      getMaxDiscountStoreOfAll(_maxDiscountStores),
      ..._maxDiscountStores
    ];
    ...
  }
  
  ...

  StoreHome? getMaxDiscountStoreOfAll(List<StoreHome?> stores) {
    ...
  }
}
```

## 문제점

1. 수직 거리 - 인스턴스 변수 🆘 `_order` 변수가 생성자 뒤에 작성되어 있음
   <br/> 위에서 사용되는 다른 변수들이 통신을 통해 별도의 초기화 과정을 진행하는 것과 달리, _order 는 특정 값으로 초기화를 진행해 이를 구분하기 위해 생성자 뒤로 위치시켰다. 하지만 지금 보니 변수가 흩어져있어서 인스턴스 변수의 파악이 어려워졌다.

2. 수직 거리 - 종속 함수 🆘 호출하는 함수와 호출되는 함수가 멀리 떨어져 있음
   <br/> 초기에 api 통신 코드와 가공 함수를 분리해서 보려다보니 `getMaxDiscountStores()` 에서 `getMaxDiscountStoreOfAll()` 를 호출하고 있음에도 불구하고 두 함수 간 수직 거리가 컸다.

## 좋았던점

1. 개념은 빈 행으로 분리하라 ✅ 각 메서드 사이 빈 행이 들어감
   <br/> 코드가 너무 붙어있으면 구분이 잘 안되는 것 같아서 빈행을 적극적으로 활용하는 편. 

2. 가로 공백과 밀집도 ✅ 할당 연산자 사이 공백
   <br/> 포맷터도 적극 사용하는 편이지만 연산자 사이에는 가독서을 위해 공백을 넣는 편.

<br/>

# 개선
```dart
/* 개선 후 */
class HomeViewModel with ChangeNotifier {
  late final HomeService _service;
  final AdminService _adminService = AdminService();

  bool _isLoading = true;
  List<Category>? _categories;
  List<Tab>? _tabs;
  List<StoreHome?> _maxDiscountStores = [];
  List<List<Menu>> _discountMenus = [];
  Order _order = Order.values.first;

  HomeViewModel(BuildContext context) {
    ...
  }

  Future<void> getMaxDiscountStores() async {
    ...
  }
  
  StoreHome? getMaxDiscountStoreOfAll(List<StoreHome?> stores) {
    ...
  }
}
```

## 🥔 두 함수 및 변수 위치 조절

* `_order` 👉 다른 변수들과 함께 위치하도록 변경
<br/>

* `getMaxDiscountStoreOfAll` 👉 `getMaxDiscountStores()` 아래로 위치 변경
<br/>

<br/>
<br/>

# 2️⃣ Flutter 가게 관리 관련 애플리케이션
```dart
/* 개선 전 */
...
  validator: (input) { return null; },
...
```

## 문제점
1. 들여쓰기 무시하기 🆘 한 줄짜리 함수에 대해 들여쓰기를 무시힘
  <br/> 추후 수정을 진행할 함수라 화살표 함수 대신 중괄호를 사용했었는데 한 줄짜리 함수라 한줄로 작성 했었다.

# 개선
```dart
/* 개선 후 */
...
  validator: (input) { 
    return null; 
  },
...
```

## 🥔 들여쓰기 사용

* 기존에 한 줄로 작성했던 코드를 들여쓰기를 넣어 변경했다.
<br/>

