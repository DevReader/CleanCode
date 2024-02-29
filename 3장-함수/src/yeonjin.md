### 사례 1 -1

```jsx
exportWorkToPDF() {
// PDF 생성 ..
// s3에 pdf 파일 업로드
    const s3Params = {
      Bucket: AWS_BUCKET_NAME,
      Body: pdfStream,
      ContentType: 'application/pdf',
    };
}
```

### 문제

함수는 한 가지만을 잘 해야 한다.

그러나 하나의 함수 안에서 여러가지 일을 하고 있다.

### 해결

S3 파일을 업로드하는 부분을 함수로 처리한다.

```jsx
exportPDFAndUploadToS3(){
// PDF 생성 ...
uploadPDFToS3(generatedPdf)
}

upLoadPDFToS3(generatedPdf){
// s3에 pdf 파일 업로드
    const s3Params = {
      Bucket: AWS_BUCKET_NAME,
      Body: generatedPdf,
      ContentType: 'application/pdf',
    };
// ...
```

### 사례 2

```jsx
filterExistingCharacter() {
	// 리스트에서 중복 제거...
	...
	// 중복 제거된 리스트에서 빈 문자열 제거
	...
```

### 문제

함수명은 중복만을 제거하는 것같지만, 실제론 필터링한 리스트에 포함된 빈 문자열도 제거하고 있다.

### 해결

```jsx
removeDuplicatesAndEmptyStrings(){
// removeExistingCharacter() -> 리스트에서 중복 제거하는 함수
// removeEmptyStrings() -> 리스트에서 빈 문자열 제거하는 함수
}
```

함수명을 적절히 변경하고 내부적인 동작을 나누어 각각 함수를 만들었다.
