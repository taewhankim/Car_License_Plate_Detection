# Car License Detection
## 한국 번호판 인식

![123가4568(1)](https://user-images.githubusercontent.com/71427403/104855588-eccc4d80-5950-11eb-9a26-8dd1cf2d9139.jpg)
![번호판](https://user-images.githubusercontent.com/71427403/104855593-fa81d300-5950-11eb-9cb7-b5e981535e7b.png)

---

## Image processing 을 통한 차량 번호판 인식

### Method
* tesseract-ocr-w64-setup-v5 압축을 풀고 설치
* [Tesseract](https://github.com/tesseract-ocr/tessdata/blob/master/kor.traineddata) 에서 **kor.traineddata** 다운로드
* 다운로드 된 **kor.traineddata** 파일을 C:/Program Files/Tesseract-OCR/tessdata 폴더로 이동


### Workflow

![adaptive threshold](https://user-images.githubusercontent.com/71427403/104856159-4f731880-5954-11eb-8eca-61a9fbb5d331.png)


1. ```GaussianBlurf``` 를 통해 노이즈를 삭제 후 Contour 형성을 위한 Binary Image 형식 변환



![contour](https://user-images.githubusercontent.com/71427403/104856160-4f731880-5954-11eb-8042-ea1de75d5aa9.png)


2. ```findContours```, ```drawContours``` 로 Contour 시각화



![박스로 변경](https://user-images.githubusercontent.com/71427403/104856164-50a44580-5954-11eb-93b0-5e8c135f49e1.png)


3. ```boundingRect```으로 Contour 위에 바운딩 박스를 시각화
> 좌상단 (x, y) 좌표
> W, H = 너비, 높이
> 중심 좌표 (cx, cy)


![dddd](https://user-images.githubusercontent.com/71427403/104856161-500baf00-5954-11eb-80fb-a0dffc22348e.png)


4. 조건에 만족하는 Contour Box 만 추출
> 넓이가 최소 80 이상
> 최소 너비, 높이 = 2, 8
> 최소 비율, 최대 비율 = 0.25, 1
> MAX_DIAG_MULTIPLYER = 대각선 길이의 배
> MAX_ANGLE_DIFF = 두 Contour Box의 중심점 각도 차이
> MAX_AREA_DIFF = 두 Contour Box의 면적 비율 차이
> MAX_WIDTH_DIFF = 두 Contour Box의 너비 비율 차이
> MAX_HEIGHT_DIFF = 두 Contour Box의 높이 비율 차이
> MIN_N_MATCHED = 위 조건을 만족한 Contour Box의 개수
> 조건에 맞는 Contour Box Index 지정

![dddw](https://user-images.githubusercontent.com/71427403/104856162-500baf00-5954-11eb-8d76-799f5b65eb99.png)


5. 기울기 조정과 tesseract를 통한 번호판 추출

> ```getRotationMatrix2D``` 추출
> ```getRotationMatrix2D``` 로 ```warpAffine``` 통한 이미지 회전
> ```getRectSubPix``` 회전된 이미지에서 조건에 따라 원하는 부분만 crop

