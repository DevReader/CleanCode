## 사례 1

### 수정 전

```jsx
// 정렬된 character list를 저장하는 변수
const characterList = …
```

→ 컨테이너 유형을 넣지 않는 것이 바람직함. 의미가 명확하지 않음.

### 수정 후

```jsx
const sortedCharacters = …
```

## 사례 2

### 수정 전

```jsx
// arrow 연결 여부를 저장하는 변수
const existingArrow1 = ..
const existingArrow2 = ..
```

→ 두 변수를 구분하기 위해 뒤에 1,2같은 의미없는 숫자를 붙임.

### 수정 후

```jsx
// arrow 연결 여부를 저장하는 변수
const existingArrowForward = ..
const existingArrowBackward = ..
```
