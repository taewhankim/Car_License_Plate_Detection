# Car License Detection
## 한국 번호판 인식

![123가4568(1)](https://user-images.githubusercontent.com/71427403/104855588-eccc4d80-5950-11eb-9a26-8dd1cf2d9139.jpg)
![번호판](https://user-images.githubusercontent.com/71427403/104855593-fa81d300-5950-11eb-9cb7-b5e981535e7b.png)

---

## Image processing 을 통한 차량 번호판 인식

### Method
* tesseract-ocr-w64-setup-v5 압축을 풀고 설치
* ![링크](https://github.com/tesseract-ocr/tessdata/blob/master/kor.traineddata) 에서 **kor.traineddata** 다운로드
* 다운로드 된 **kor.traineddata** 파일을 C:/Program Files/Tesseract-OCR/tessdata 폴더로 이동



![adaptive threshold](https://user-images.githubusercontent.com/71427403/104855672-5fd5c400-5951-11eb-9823-f0e680adbc67.png)

1. Binary Image 형식으로 변환시킨다.

![contour](https://user-images.githubusercontent.com/71427403/104855838-80eae480-5952-11eb-8282-45b6018e1e81.png)

2. Contour로 변환시킨다.

![박스로 변경](https://user-images.githubusercontent.com/71427403/104855840-85170200-5952-11eb-8365-692e5e075297.png)

3. Contour로 나타낸 이미지를 rectangular 시킨다. 

![dddd](https://user-images.githubusercontent.com/71427403/104855931-e5a63f00-5952-11eb-9e71-717785ca0f43.png)

4. 조건에 만족하는 Contour Box 만 추출

![dddw](https://user-images.githubusercontent.com/71427403/104855970-27cf8080-5953-11eb-9cd0-d0ca4e023d6f.png)

5. 기울기 조정과 tesseract를 통해 번호판 추출

