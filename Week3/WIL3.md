<h2> Computer Vision </h2>
inverse computer graphics
<h3> Image classification </h2>

 - Classifier

    > input ( image ) --[classifier]--> output ( label )
    
- semantic gap: 컴퓨터와 인간이 보는 이미지가 다름. 

<h3> KNN </h3>

- 훈련단계: 모든 데이터 기억
- 예측단계: 새로운 이미지를 보고 훈련단계에서 본 이미지 중 가장 유사한 이미지를 찾아 라벨을 예측

    - 데이터 사이의 거리를 구해 유사도 추측
    - 픽셀의 rgb값 차이로 거리 측정
    - 거리는 유클리드 거리나 맨헤튼 거리(택시거리)를 사용
    - 이웃의 수 K의 값을 변화하여 다수결을 통해 출력 결정

- KNN의 단점
    
    1. 시간이 너무 오래 걸림
    2. 픽셀끼리 거리가 이미지의 시각적 유사성과 일치하지 않음
    3. 차원의 저주

        > 차원이 커지면 학습데이터도 기하급수적으로 커지게 되는 문제
    
<h3> Linear Classification </h3>

- Parametric Approach

    > 1차함수로 점수를 산출해서 분류

    $f(x, W) = Wx + b$

    x: input\
    W: weight\
    b: bias\
    f: class scores

    하나로만 요약되어버리는 단점이 있음 $\rarr$ 여러 분류기를 쌓아야 함

<h3> Loss function </h3>

> 모델(분류기) 성능의 지표
    
- SVM Loss
    > $L_i=\sum_{j\neq y_i}\text{max}(0,s_j-s_{yi}+\Delta)$

    $s_j$ = j일 가능성 점수\
    $S_{y_i}$ = 답일 가능성 점수\
    $\Delta$: 답이 아닌 점수가 답인 점수보다 최소한 이정도만큼은 작아야 한다는 뜻

    >$\text{SVM Loss }L=\frac{1}{N}\sum_{i=1}^N\sum_{j\neq y_i}\text{max}(0,f(x_i;W)_{j}-f(w_i;W)_{y_i}+\Delta)$\
    점수차 + 델타 의 평균

    정규화
    - L2 Regularization
        >$Cost=\frac{1}{n}\sum_{i=1}^n\{L(y_i,\hat{y_i})+\frac{\lambda}{2}|w|^2\}$

        - 매끄러운 그래프
        - 모든 요소의 전체적인 영향

    - L1 Regularization\
        >$Cost=\frac{1}{n}\sum_{i=1}^n\{L(y_i,\hat{y_i})+\frac{\lambda}{2}|w|^2\}$

        - 분류기가 복잡할 때 씀
        - 더 단순한 식

