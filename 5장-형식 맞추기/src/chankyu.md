# 5장 혐식 맞추기

## 수정 전
```js
function solution(s)
{
  function oddCenter(index, size) {
        if(index - size < 0 || index + size >= s.length) return size;
        if(s[index-size] === s[index+size]) {
            return oddCenter(index, size+1);
        }
        return size;
    }
    function evenCenter(index1, index2, size) {
        if(index2 >= s.length || s[index1] !== s[index2]) return 0;
        if(index1-size < 0 || index2 + size >= s.length) return size;
        if(s[index1-size] === s[index2+size]) {
            return evenCenter(index1, index2, size+1);
        }
        return size;
    }
    let max = 0;
    for(let i=0;i<s.length;i++){
        max = Math.max(oddCenter(i, 1) * 2 - 1, max);
        max = Math.max(evenCenter(i, i+1, 1) * 2, max);
    }
    return max;
}
```

### 반대로 읽어야 함
- main 함수에서 함수를 호출하기전에 함수를 선언하고 있다.
- 선언된 함수가 어떻게 사용될지 예상하며 훑어 본 후, main을 확인하고 다시 함수의 내부 구현을 확인해야 한다.

### 분리되지 않은 개념
- 각 함수, 변수 선언부 및 main 로직에 빈 행이 없어 가독성을 저하하고 있다.

## 수정 후
```js
function solution(s)
{
    let max = 0;

    for(let i=0;i<s.length;i++){
        max = Math.max(oddCenter(i, 1) * 2 - 1, max);
        max = Math.max(evenCenter(i, i+1, 1) * 2, max);
    }
    
    function oddCenter(index, size) {
        if(index - size < 0 || index + size >= s.length) return size;
        if(s[index-size] === s[index+size]) return oddCenter(index, size+1);
        
        return size;
    }
    
    function evenCenter(index1, index2, size) {
        if(index2 >= s.length || s[index1] !== s[index2]) return 0;
        if(index1-size < 0 || index2 + size >= s.length) return size;
        if(s[index1-size] === s[index2+size]) return evenCenter(index1, index2, size+1);
        
        return size;
    }

    return max;
}
```

### 한줄 {}블록에 대한 생각
- 생략시 코드가 간결해지고, 가로 길이가 적절할 경우 가독성이 좋아진다.
- 생략시 새로 코드를 추가해야할 상황에서 버그가 발생할 가능성이 있다.
- 프로젝트나 팀의 일관성에 맞게 사용하는 것이 적절하고, 규모가 큰 프로젝트일수록 생략하지 않는 것이 일관성을 유지하기 좋아보인다.