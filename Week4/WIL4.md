<style>.katex { font-size: 2em !important; } </style>
<h1> Object detiction </h1>

* Image classification 과 다른점
   - Object detection은 이미지 하나에 라벨 여러개
   - Object detection은 분류라벨 말고도 위치정보 (bbox)도 줘야함



<h3> Sliding Window </h3>
 
 이미지를 window로 픽셀단위로 훑으면서 전수조사하는 방법
   $\rarr$ 너무 느림


<h2> R-CNN </h2>

 - selective search로 ROI(Region Of Interest) 추출
 - 일정한 크기로 warping
 - CNN feature 계산
 - SVM으로 분류
 - Bounding Box Regresser로 위치 예측
    - bounding box 의 위치가 정확한지는 IoU로 계산하여 측정
    - $\text{IoU}=\frac{A\cap B}{A\cup B}$
 - Nom Maximum Supression으로 중복되는 박스 제거

 <h3> Object detector 평가 </h3>

 - Confidence
 - Mean Average Precision

<h2> Fast R-CNN </h2>

 - Selective Search를 하지 않고 한번의 CNN으로 대체
 - ROI추출을 ROI pooling으로 대체
 - 분류 방법로 SVM대신 Linear
 - bbox regressor와 classifier를 하나의 네트워크로 통합


<h2> Faster R-CNN </h2>

 - Anchor Box 도입
 - Selective Search 대신 RPN추가
    - CNN으로 feature map을 얻음
    - feature map으로 region proposal network를 거쳐 region proposal함
    - ROI pooling을 거쳐 분류하고 위치 찾음(bbox)
    - 두 작업을 하나의 피쳐맵에서 정보를 받아서 처리하므로 end-to-end로 전체 네트워크를 학습시킬 수 있게됨


<h2>mean Average Precision</h2>

 - Precision Recall
   |실제 상황|Positive|Negative|
   |:-:|:-:|:-:|
   |Positive|<b>T</b>rue <b>P</b>ositive|<b>F</b>alse <b>N</b>egative|
   |Negative|<b>F</b>alse <b>P</b>ositive|<b>T</b>rue <b>N</b>egative|
   > True / False : 옳은 검출 / 옳지 않은 검출<p>
   Positive / Negative : 검출됨 / 검출 안됨
   
   <h3>Precision</h3>
   검출된 것들 중 옳은 검출

   >$Precision=\frac{TP}{TP+FP}$

   <h3>Recall</h3>
   실제로 옳은 케이스 중 검출해낸 케이스

   >$Recall=\frac{TP}{TP+FN}$

   <h3>Confidence</h3>
   프로그램이 이 예측이 얼마나 정확한지 알려주는 수치

   
   <h3>Precision-Recall curve</h3>

    전체 검출 결과를 confidence로 내림차순 정렬하고 위에서부터 차례대로 누적된 검출 결과를 토대로 Precsion과 Recall을 계산하여 이를 그래프로 나타냄

   <h3>Average Precision</h3>
    
    P-R curve의 아래 면적

   <h3>mean Average Precision</h3>

    각 클래스의 AP를 모두 더해 클래스 개수로 나눠준 값
    
    >$\text{mAP}=\frac{1}{N}{\sum \limits_k^N AP_k}$
