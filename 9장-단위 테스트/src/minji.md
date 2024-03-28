# 실습 - Flutter 카운터

```dart
/* 개선 전 */
class Counter {
  int value = 0;

  void increment() {
    value++;
  }

  void decrement() {
    value--;
  }
}
```

## 문제점

- 코드 수정시, 안정성을 확인할 방법이 없어서 의도하지 않은 결함률이 증가
- 코드 변경 유연성 부족

<br/>

# 실습 - 개선

```dart
/* 개선 후 */
void main () {
  group('Counter', () {
      test('value should start at 0', () {
        expect(Counter().value, 0);
      });

      test('value should be incremented', () {
        final counter = Counter();

        counter.increment();
        expect(counter.value, 1);
      });

      test('value should be decremented', () {
        final counter = Counter();

        counter.decrement();
        expect(counter.value, -1);
      });
    });
}
```

## 🥔 테스트 코드 넣기

- 카운터 버튼에 대한 테스트 코드를 추가함
- increment 와 decrement 가 정상적으로 수행되는지, 초기 값이 0으로 잘 초기화 되는지 확인함
