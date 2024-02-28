# 2장 의미 있는 이름
## 내용 정리
### 의도를 분명히 밝힌다
- **기능**, **사용 방법**이 명확하다

### 의미 있는 맥락을 추가한다
- 클래스에 넣는다
- 접두어를 추가한다 (불필요한 맥락은 추가하지 않는다)

### 검색하기 쉬운 이름을 사용한다
- 상수에 이름을 붙인다

### 관습을 따른다
- 클래스 이름은 명사
- 메서드 이름은 동사

### 같은 개념은 표현을 통일한다
- ex. Driver, Manager, Controller

### 그릇된 정보는 없앤다
- 기존에 널리 이용되는 의미와 다른 의미의 단어 ex. hp
- List 자료구조가 아니라 복수를 표현하는 list
- 비슷해서 혼동을 주는 이름

### 의미 없는 정보는 없앤다
- 연속된 숫자 덧붙이기 ex. element1, element2
- 불용어를 추가한 이름 ex. Product**Info**, name**String**

## 사례 적용
### 사례 1
**Before**
```
// 리소스를 연결하고, 전역 변수를 초기화한다
initializeVariables()
```
→ 의미가 분명하지 않음</br></br>
**After**
```
// 리소스를 연결한다
inflateResource()

// 전역 변수를 초기화한다
initializeGlobalVariables()
```
### 사례 2
**Before**
```
// 유저가 입력한 페이지를 얻는다
Integer getCurrentPage() { ... }
```
→ current page가 무슨 뜻인지 추론이 필요함</br></br>
**After**
```
Integer getSelectedPage() { ... }
```

### 사례 3
**Before**
```
// 교재 버튼을 클릭하면
// 클릭한 교재 버튼의 스타일을 바꾸고
// 해당 교재의 첫 페이지에 있는 문제 리스트를 보여준다.
setOnClickListenerToBookBtn(book);
```
→ 주석을 통해 기능 설명</br></br>
**After**
```
View.OnClickListener listener = clickedView -> {
    setClickedStyle(clickedView);
    showProblemsInFirstPageOf(book);
};
bookBtn.setOnClickListener(listener);
```
→ OnClickListener의 기능을 간략하게 정리</br></br>

### 사례 4 ❓
**Before**
```
val problemsOnSelectedBook = getProblemsOnSelectedBook(problems!!)
val problemsOnSelectedPage = getProblemsOnSelectedPage(problemsOnSelectedBook)

fun getProblemsOnSelectedBook(problems: List<Problem>) {
    return problems.filter { it.bookId == book?.id }
}
    
fun getProblemsOnSelectedPage(problems: List<Problem>) {
    return problems.filter { it.page == page }
}
```
→ 명령형으로 구성</br></br>
**After**
```
val problemsOnSelectedPage = problems!!
        .onBook(bookInfo!!.selectedBook)
        .onPage(bookInfo!!.selectedPage)
        
fun List<Problem>.onBook(book: Book?) = filter { it.bookId == book?.id }
fun List<Problem>.onPage(page: Int?) = filter { it.page == page }
```
→ 함수형으로 구성</br></br>
