<style>.katex { font-size: 1.5em !important; } </style>
<h1>Semantic Segmentation</h1>

  * Segmentation: 이미지의 각 픽셀이 뭔지 파악하고 라벨을 메김
    * Instance Segmentation: class가 같은 instance끼리도 구분
    * Semantic Segmentation: instance를 구분하지 않고 라벨링만 함

<h2>FCN</h2>

> Fully Convolutional Network
* 특징
    1. VGG16을 backbone으로 사용
        > backbone: 모델의 기본모델(?)
    2. VGG 네트워크의 FC Layer인 nn.Linear 부분을 Convolution으로 변경
    3. Transposed Convolution을 이용해 Pixel-wise Prediction을 수행

    > VGG net: 크게 5번의 Max Pooling 후 FC layer를 하는 모델

    VGG net을 backbone으로 사용하고 마지막 FC layer를 FCN으로 대체하여 공간정보를 보존하고 임의의 입력값에 대해서도 학습이 가능해짐

    Max Pooling을 5번 하여 크기가 32배 축소되는데 마지막에 입력과 같은 크기로 만들어주기 위해 Upsampling을 함.
    <h3>Upsampling</h3>

    * Unsampling: Max Pooling에서 Pooling을 하는 위치를 기억해놓고 그 위치에 피쳐맵의 값을 넣고 나머지 위치에는 0을 집어넣음
    * Bilinear Interpolation: 2차원 선형보간
    
    FCN에서는 이같은 정적인 방식이 아닌 학습을 통해 결정하는 편이 좋음 $\Rarr$ Transposed Convolution을 통해 Pixel-wise prediction을 진행함

    <h3>Transposed Convolution</h3>

        convolution연산의 반대과정. 작은 행렬을 커널을 이용해 큰 행렬로 확장

        feature map을 다시 입력값으로 되돌리는게 목적이 아니므로 transpose는 reverse연산이 아님

        원래 convolution연산은 kernel을 입력 크기로 적당히 0을 채우고 이를 flatten하고 쌓아서 희소행렬 C를 만든 후 입력을 열벡터로 flatten한 것과 곱을 계산한 것.

        Transpose convolution은 C행렬을 Transpose한 전치행렬을 곱함.

    <h3>FCN 성능 향상방법</h3>
    앞선 레이어의 feature맵을 이용하여 정확도를 높일 수 있음

    * Pixel Accuraccy\
    >$\text{Pixel Accuracy}=\frac{\text{True}}{\text{Total}}$

    <h3>FCN의 한계</h3>
    1. 객체의 크기가 크거나 작은 경우 성능이 떨어짐
    2. Object의 디체일한 모습을 반영 못함

    <h3>DeconvNet</h3>

    FCN의 한계를 극복하기 위해 Encoder - Decoder 구조 사용
    convolution 연산과 upsampling 연산이 대칭되기 때문에 같은 수의 pooling (max pooling & unpooling)과정을 둠
