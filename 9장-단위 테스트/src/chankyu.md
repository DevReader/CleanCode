# 9장 단위 테스트

## 테스트 코드가 사라지고 팀 생산성이 떨어지는 과정
1. 실제코드가 변경되면 테스트코드도 변경되어야 한다.
2. 테스트 코드가 지저분하면 테스트코드를 변경하기 어렵다.
3. 지저분한 테스트 코드 때문에 테스트를 통과시키기 너무 어렵고, 테스트 코드는 계속 늘어난다.
4. 점차 테스트 코드는 개발자 사이에서 가장 큰 불만이 된다.
5. 테스트 코드를 폐기한다.
6. 테스트 코드가 없으면 코드를 수정할 때 잘 작동하는지 검증할 방법이 없다.
7. 더 이상 코드를 수정하지 않는다.

## 테스트당 assert 하나

### before

```ts
describe("Navigator Component", () => {
  it("정상적으로 렌더링되고 라우팅되어야 함", async () => {
    const mockPath = "/test-path";
    const mockText = "Test";
    render(
      <NavigationBarItem
        path={mockPath}
        SelectedIcon={MockSelectedIcon}
        Icon={MockIcon}
        text={mockText}
      />
    );
    const item = screen.getByText(mockText);
    expect(item).toBeInTheDocument();
    fireEvent.click(item);
    expect(mockNavigate).toHaveBeenCalledWith(mockPath);
  });
});
```

- 동작의 효율성을 생각해서 하나로 합친 테스트.
- 테스트는 자원이 제한적이지 않다. 효율보단 개념 분리를 더 우선적으로 고려하자.

### after

```ts
describe("Navigator Component", () => {
  const mockPath = "/test-path";
  const mockText = "Test";
  beforeEach(() => {
    render(
      <NavigationBarItem
        path={mockPath}
        SelectedIcon={MockSelectedIcon}
        Icon={MockIcon}
        text={mockText}
      />
    );
  });

  it("정상적으로 렌더링되어야 함", async () => {
    const item = screen.getByText(mockText);
    expect(item).toBeInTheDocument();
  });

  it("정상적으로 라우팅되어야 함", async () => {
    const item = screen.getByText(mockText);
    fireEvent.click(item);
    expect(mockNavigate).toHaveBeenCalledWith(mockPath);
  });
});
```
