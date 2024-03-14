# 5장 형식 맞추기

## 내용 정리

### 적절한 길이 유지하기
- 파일: __500__ 줄 이하
- 가로: __120__ 자 이하
<br/>

### 가까운 개념은 가깝게
- __지역 변수__ 는 범위의 맨 위에
- __필드__ 는 클래스 맨 위에
- __종속 함수__ 는 호출하는 함수 바로 아래에
<br/>

## 실습
### 사례 1
- 들여쓰기 __무시__
```
if (isDeleteBookBtnVisible()) toggleVisibilityOfDeleteButton()
```
<br/>

- 들여쓰기 __적용__
```
if (isDeleteBookBtnVisible()) { 
    toggleVisibilityOfDeleteButton()
}
```
