### TDD 법칙 세 가지

- 첫째: 실패하는 단위 테스트를 작성할 때가지 실제 코드를 작성하지 않는다.
- 둘째: 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
- 셋째: 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

테스트 코드가 실제 코드보다 불과 몇 초 전에 나온다.

방대한 테스트 코드는 심각한 관리 문제를 유발한다.

### 깨끗한 테스트 코드 유지하기

테스틑 코드가 복잡할수록 실제 코드를 짜는 시간보다 테스트 케이스를 추가하는 시간이 더 걸린다.

의도하지 않은 결함 수가 많아지면 개발자는 변경을 주저한다.

- 테스트는 유연성, 유지보수성, 재사용성을 제공한다.
  - 단위 테스트 → 테스트 케이스가 있으면 변경이 쉬워진다.

### 깨끗한 테스트 코드

가독성 → 명료성, 단순성, 풍부한 표현력

- 도메인에 특화된 테스트 언어
- 이중 표준

### 테스트 당 assert 하나

given-when-then 함수 이름

테스트를 분리하면 중복되는 코드가 많아진다.

template method 패턴을 사용하면 중복을 제거할 수 있음

given/when 부분을 부모 클래스에 두고 then 부분을 자식 클래스에 두면 된다.

독자적인 테스트클래스를 만들어 before 함수에 given/when 부분을 넣고 test 함수에 then 부분을 넣는다.

- 테스트 당 개념 하나

### FIRST

- 테스트는 빨라야 한다.
- 각 테스트는 의존하면 안 된다. 순서가 존재하면 안 됨 (독립적으로)
- 테스트는 어떤 환경에서도 반복 가능해야 한다. (반복가능하게)
- 테스트는 부울 값으로 결과를 내야 한다. (자가검증하는)
- 테스트는 적시에 작성해야 한다. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다. (적시에)

### 결론

테스트 API를 구현해 **도메인 특화 언어**를 만들자.

테스트 코드가 방치되면 실제 코드도 망가진다. ‘변경’할 수 있는 코드.

### 궁금했던 점

- TDD로 개발하는 개발자의 효율에 대해서?
  - 어떤 상황에서 TDD를 사용하는 게 좋을까? 조프로젝트 규모, 기간 ..
- 이미 작동하고 있는 코드에 대해서 테스트 코드를 작성하는 것?

### 실습

```js
// ...

  it('should return works by category', async () => {
    const uid = 'user_id';
    const category = 'category';
    const expectedWorks: GetWorkDto[] = [
      // 예상 값 리스트
    ];

    (workModel.aggregate as jest.Mock).mockReturnValueOnce(expectedWorks);

    const result = await workService.getWorksByCategory(uid, category);

    expect(result).toEqual(expectedWorks);
    expect(workModel.aggregate).toBeCalledWith([
      {
        $match: {
          author: uid,
          category: category,
        },
      },
      // ...
    ])
  });
});

// ...
```

문제: 테스트할 수 있는 코드가 존재하지 않음

→ jest를 사용해서 nestjs의 함수를 테스트하는 파일을 생성
