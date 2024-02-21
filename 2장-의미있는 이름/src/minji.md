# 1️⃣ BOJ 2251번 물통에 대한 풀이 코드

[문제 바로가기](https://www.acmicpc.net/problem/2251)

```python
# 개선 전
maxA, maxB, maxC = map(int, input().split())
cases = []
answer = []


def dfs(A, B, C):
    global cases, answer, maxA, maxB, maxC

    if [A, B, C] in cases:
        return

    cases.append([A, B, C])

    if A == 0:
        answer.append(C)

    if A != 0:
        # b에게 주기
        if A >= maxB-B:
            dfs(A-(maxB-B), maxB, C)
        else:
            dfs(0, B+A, C)
        # c에게 주기
        if A >= maxC-C:
            dfs(A-(maxC-C), B, maxC)
        else:
            dfs(0, B, C+A)
    if B != 0:
        # a에게 주기
        if B >= maxA-A:
            dfs(maxA, B-(maxA-A), C)
        else:
            dfs(A+B, 0, C)
        # c에게 주기
        if B >= maxC-C:
            dfs(A, B-(maxC-C), maxC)
        else:
            dfs(A, 0, C+B)
    if C != 0:
        # a에게 주기
        if C >= maxA-A:
            dfs(maxA, B, C-(maxA-A))
        # b에게 주기
        else:
            dfs(A+C, B, 0)
        if C >= maxB-B:
            dfs(A, maxB, C-(maxB-B))
        else:
            dfs(A, B+C, 0)


dfs(0, 0, maxC)
answer.sort()
print(*answer)

```

## 문제점

1. 중복 줄이기 🆘 내부에 있는 if 문들은 A,B,C 변수만 다를뿐 완전히 동일하고 중복된 코드
   <br/> 당시 **급하게** 문제를 푼다고 이렇게 썼다. 실수가 나지 않을까 조마조마해하며..

2. 자신의 기억력을 자랑하지 않기 🆘 A, B, C 와 같은 문자 하나 짜리 변수명
   <br/> 문제에서 주어진 값을 그대로 쓰다보니 무심코 A,B,C 로 네이밍 한 부분이 있다.

## 좋았던점

1. 그릇된 정보 피하기 ✅ caseList 대신 cases 사용
   <br/> 기존엔 `List` 라는 네이밍을 정말 좋아했었는데, Kotlin 을 하면서 List 가 아닌 곳에도 List 를 사용하는 것을 보고 고쳐야겠다고 생각한 습관. 대신 뒤에 s 를 붙여 복수의 데이터를 의미하게끔 하고 있음

2. 해당 영역에서 가져온 이름 쓰기 ✅ dfs 라는 함수명 사용
   <br/> 코딩테스트 한정, 좋은 이름이지 않나 싶다. 알고리즘 명을 함수에 직접 넣어 어떤 알고리즘을 통해 문제를 해결했는지 보여준다.

<br/>

# 개선

```python
#개선 후
maxA, maxB, maxC = map(int, input().split())
cases = []
answers = []


def pour(source, destination, destinationMax):
    pourAmount = min(source, destinationMax-destination)
    return source-pourAmount, destination+pourAmount


def dfs(waterA, waterB, waterC):
    global cases, answers, maxA, maxB, maxC

    if [waterA, waterB, waterC] in cases:
        return

    cases.append([waterA, waterB, waterC])

    if waterA == 0:
        answers.append(waterC)

    if waterA != 0:
        sourceA, destinationB = pour(waterA, waterB, maxB)
        dfs(sourceA, destinationB, waterC)

        sourceA, destinationC = pour(waterA, waterC, maxC)
        dfs(sourceA, waterB, destinationC)

    if waterB != 0:
        sourceB, destinationA = pour(waterB, waterA, maxA)
        dfs(destinationA, sourceB, waterC)

        sourceB, destinationC = pour(waterB, waterC, maxC)
        dfs(waterA, sourceB, destinationC)

    if waterC != 0:
        sourceC, destinationA = pour(waterC, waterA, maxA)
        dfs(destinationA, waterB, sourceC)

        sourceC, destinationB = pour(waterC, waterB, maxB)
        dfs(waterA, destinationB, sourceC)


dfs(0, 0, maxC)
answers.sort()
print(*answers)
```

## 🥔 중복 줄이기

```Python
if A >= maxB-B:
  dfs(A-(maxB-B), maxB, C)
else:
  dfs(0, B+A, C)
```

위 코드가 계속해서 반복되는 것 같아서 이부분을 함수로 변경했다.

```Python
def pour(source, destination, destinationMax):
    pourAmount = min(source, destinationMax-destination)
    return source-pourAmount, destination+pourAmount
```

## 🥔 A, B, C 네이밍 바꾸기

`A,B,C` 👉 `waterA, waterB, waterC`

문제에서 각 값을 A,B,C 라고 주었기 때문에 A,B,C 를 활용하면서도 한 글자는 아니도록 변경하고 싶었다.

물이라는 걸 알려주도록 water 을 붙이기로 선택했다.

<br/>
<br/>

# 2️⃣ Flutter 판매 관련 애플리케이션, API 통신 코드

```dart
/* 개선전 */
Future<List<StoreSimple>> getStores(LatLng position) async {
  ...생략...
}

Future<Store> getStore(int id) async {
  ...생략...
}
```

## 문제점

1. 그릇된 정보 피하기 🆘 getStores 와 getStore 와 같은 너무 흡사한 함수명
   <br/> 심지어 getStores 는 사용자의 위치를 기반으로, getStore 는 가게 id 를 통해 가게를 조회 중이다.

## 좋았던점

1. 한 개념에 한 단어 쓰기 ✅ get, fetch 등 섞어 쓰지 않고 우직하게 get~ 사용
   <br/> 예전 애플리케이션 코드 중에 get, fetch 를 야무지게 섞어서 사용하다가 대규모 리팩토링을 한 경험이 있어서 우직하게 get 을 쓰기 시작했다.

<br/>

# 개선

```dart
/* 개선후 */
Future<List<StoreSimple>> getNearStores(LatLng position) async {
  ...생략...
}

Future<Store> getStoreById(int id) async {
  ...생략...
}
```

## 🥔 그릇된 정보 피하기

`getStores` 👉 `getNearStores`

유저의 위치를 기반으로 근처 가게들을 가져오는 함수이므로 Near 를 추가해주었다.

`getStore` 👉 `getStoreById`

딱 하나의 Store 를 Id 를 통해 조회하는 함수라 ById 를 붙여줬고, 추후 Name 이나 다른 요소들로 조회하는 함수가 생긴다면 By~ 로 일관성있게 작성할 수 있을 것 같아 선택했다.

<br/>
<br/>

# 3️⃣ Android 판매 관련 애플리케이션, 모델 및 클래스

```kotlin
/* 개선전 */
data class MartItemDTO()

data class ItemDTO()

data class Item()

data class DibsProduct()

class FollowResponseDTO()
...
```

## 문제점

1. 한 개념에 한 단어 쓰기 🆘 Mart, Store / Item, Product 등 같은 개념을 다른 단어로 사용
   <br/> 여러 명이, 급하게 작성한 코드라 일관성 없는 네이밍이 많았다.

2. 불 필요한 맥락 없애기 🆘 DTO, Response 등을 난사

<br/>

# 개선

## 🥔 한 개념에 한 단어 쓰기
* Store, Mart 👉 Mart
* Product, Item 👉 Product
* Dibs, BookMark, Follow, Favorite 👉 Dibs
* img, image, profile 👉 img

같은 개념의 단어를 한가지로 통일해 작성했다.

## 🥔 불 필요한 맥락 없애기
* DTO, Response 등을 이름에서 제거했다.