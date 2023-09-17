* 딥러닝은 AI의 하위분류인 머신러닝의 하위분류. 신경망(Neural Netework)을 기반으로 함
* 딥러닝의 구성요소: 데이터, 모델, 손실함수, Optimization and Regularization
1. 모델
    * 데이터를 학습하는 부분
        * 합성곱 신경망, CNN
            >FNN에서 인접 픽셀의 정보를 무시하여 정보 손실이 발생하는 문제를 해결
        
            >주변 픽셀을 포함해 Convolution을 계산하여 공간정보 유지함
        * AlexNet
            > Relu, Data augmentation, Dropout 사용
        * VGGNet
            > 5*5 컨볼루션 필터를 3*3 필터 두개로 대체하여 연산량 줄임
        * GoogleNet
            > 1*1 컨볼루션 사용
        * ResNet
            > 신경망이 깊어지면 역전파 과정에서 가중치 갱신이 멈추는 문제를 Skip Connection으로 해결
2. Loss Function의 모순(?)
    * Multi Layer Perceptron에서 학습데이터에만 맞춰 학습되는 문제가 있음
    * 이를 해결하기 위해 일반화 과정 필요
    * 일반화 성능 = |Test error - Training error|
    * Underfitting(학습데이터도 다 모름), Overfitting(학습데이터만 앎)
    
4. Generalization
    1. 교차검증
    2. Ensemble; Bagging / Boosting
    3. Regularizing
        * Early stopping
        * Parameter norm penalty
        * Data augmentation (ex. 사진으로 돌리고 자르고 확대하고...)
                > Noise robustness = 노이즈가 있어도 결과에 큰 영향 없음
        * Dropout (학습 단계에서만 일부 노드 제외)
        * Label smoothing (모델이 너무 확신을 갖지 않도록?)
                > 과적합 방지를 위해 확률을 1로 계산하지 못하게 함
        
        
Parameter 계산하기
        > (필터크기 * 이전 레이어 feature map 개수 + 1) * (다음 레이어 feature map 개수)