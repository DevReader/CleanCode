## 5장 - 형식 맞추기

### 사례 1

```jsx
addCharacterToPevent() {
...
}

... (character와 상관없는 다른 함수들..)

getRelatedCharacter(peventText: string) {
...
}
```

### 문제

character와 plot event 연결과 관련된 함수(유사한 일을 하는 함수)가 멀리 떨어져서 구현되어 있었다.

### 해결

```jsx
addCharacterToPevent() {
...
}

getRelatedCharacter(peventText: string) {
...
}

... (character와 상관없는 다른 함수들..)
```

위치 조정: 연관성이 높은 함수를 서로 가까운 곳에 위치시켰다.
