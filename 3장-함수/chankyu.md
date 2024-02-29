# 3장 함수
클린코드 3장, 4장이 특히 논란이 많이되는 부분인 것 같습니다.

### 수정 전
```js
const makeHeader = (columnNames) => {
	const headerSection = document.createElement('thead')
	const header = document.createElement('tr');
	columnNames.forEach((column) => {
		const columnName = document.createElement('th')
		columnName.innerText = column;
		header.append(columnName);
	})
	headerSection.append(header);

	return headerSection;
};
```

### 수정 후
```js
const makeHeader= (columnNames) => {
	const header = document.createElement('tr');
	columnNames.forEach((column) => {
		const columnName = document.createElement('th')
		columnName.innerText = column;
		header.append(columnName);
	})

	return header;
}

const makeHeaderSection = (columnNames) => {
	const headerSection = document.createElement('thead')
	const header = makeHeaderColumn(columnNames);
	headerSection.append(header);
	
	return headerSection;
};
```
### 추상화 수준
- 추상화 수준을 어떻게 생각하는지에 따라 몇가지 일을 하는지가 달라진다.
	1. 헤더를 만든다
	2. 헤더 섹션을 만든다 -> 헤더를 만든더 -> 헤더에 들어갈 칼럼을 만든다
- 헤더에 들어갈 칼럼을 만드는 작업을 추상화하는 것은 적절해 보이지만, headerSection의 생성은 굳이 추상화할 작업이 아니다.
- headerSection의 생성 추상화 수준과 headerColumn을 만드는 추상화 수준은 달라진다. 그렇지만 추상화 수준을 통일하기 위해 불필요한 추상화, 함수를 만들 필요는 없다고 생각한다.

### 이름 변경
- makeHeader와 makeHeaderSection가 하는 일을 하나로 줄이니 이름도 더 명확하게 바꿀 수 있어졌다.

### 부수효과
- 순수함수로 구현이 가능한 상황에서는 순수함수로 만드는 것이 좋다.
- makeHeader에서 header를 인수로 받지 않고 내부에서 만들어 return하면 부수효과가 없어진다.