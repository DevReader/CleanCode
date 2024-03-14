### 사례1

외부 패키지 ‘pdfkit’을 사용하면서 학습 테스트를 작성하지 않음.

### 추가

```js
const fs = require("fs");
const PDFDocument = require("pdfkit");

function generatePDF(filename) {
  const doc = new PDFDocument();
  const stream = fs.createWriteStream(filename);

  doc.pipe(stream);

  doc.fontSize(20).text("Print string", 100, 100);

  doc.end();

  console.log(`PDF generated successfully: ${filename}`);
}

// 테스트 실행
const filename = "test.pdf";
generatePDF(filename);
```

간단한 테스트 코드를 작성함으로써 외부 패키지를 제대로 이해하는 과정을 거침.

→ 새로운 버전에서의 호환을 확인할 수 있는 용도로 적당한 테스트인 것 같음.
