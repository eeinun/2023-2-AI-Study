<h2> Computer Vision </h2>

* Segmentation
	* Semantic segmentation: 대상이 무엇인지만 구분
	* Instance segmentation: 대상을 다른 것들과 구분
* CNN과 FCN
	* CNN은 마지막 레이어인 FC 레이어에서 공간정보 무시됨
	* FCN은 컨볼루션으로 공간정보를 보존하고 업샘플링으로 입력과 같은 크기의 아웃풋 출력함
	* 업샘플링: Deconvoution, Interpolation ...
* Object Detection
	* 사진 속 객체를 찾아 bounding box로 표시하는 작업
		1. R-CNN: 물체가 있을만한 부분을 잘라(region propsals) CNN에 넣는 것을 2000번 수행
		2. SPPNet: Region proposals 과정을 한번의 CNN 처리로 대체함. 여기서 2000개 영역의 피쳐값을 그대로 넘겨주므로 신경망을 한번만 사용하면 됨.
		3. Fast R-CNN: spatial pyramid pooling이 느린 단점을 해결하기 위해 다양한 크기의 region을 고정된 피쳐값으로 만드는 ROI pooling으로 대체하고 region proposal 외의 모든 작업을 하나의 네트워트로 통합시킴.
		4. Faster R-CNN: Region Proposal Network 도입. 어떤 영역에 물체가 정말 있는지 계산해주는 네트워크.
		5. YOLO: bounding box를 뽑는 단계 없음. 그리드로 나누고 bounding box를 예측하면서 동시에 class probability map으로 class를 분류함. NMS 알고리즘으로 최종 결과 출력.
<h2> Pytorch </h2>

* nn.Module
  * 딥러닝 구성 레이어의 base 클래스
  * Input, Output, Forward, Backward, Parameter 정의
    * Backward: 모듈의 역전파에 사용
  * 모듈들 조합하여 모델 구성
* Dataset
  * python class 구성
    ```python
    from torch.utils.data import Dataset

    class CustomDataset(Dataset):
    def __init__(self):
        """
        데이터를 초기화
        원본 파일에서 불러오고 전처리
        """

    def __len__(self):
        """
        데이터셋의 크기를 리턴
        데이터로더가 이 값을 기준으로 돌아감
        """

    def __getitem__(self, idx):
        """
        데이터셋을 인덱싱할 수 있게 함
        데이터로더가 이걸로 데이터를 불러옴
        """
    ```
* Dataloader
  * ```python 
    from torch.utils.data import DataLoader
    ```
  * 생성자 파라미터 (일부)
    1. dataset: 만들어 둔 데이터셋 (필수)
    2. batch_size=1: 한번의 로드에 몇개의 데이터를 넣을지 결정
    3. shuffle=True: 로드할때 데이터셋을 섞을지 결정
    4. num_workers=0: 데이터 로딩에 사용하는 서브프로세스 개수 지정. 많을수록 로딩이 빠르지만 더 많은 리소스 사용. window에서는 0 초과인 경우 에러남..
    5. drop_last: 마지막 batch가 batch_sizes보다 작은 경우 이를 사용할지 결정.
* torchvision.transforms
  * PIL 객체로 이미지 받을 수 있음
  * 이미지를 가공할 수 있는 기능 제공
  * 제공하는 함수
    1. ```python
       Resize(size, ... )
       ```
       이미지 크기를 조정하는 함수.\
       size로 정수를 넣으면 가로세로 중에서 작은 쪽 크기를 이 값으로 바꾸고 sequence 자료형으로 받으면 (세로, 가로)로 인식함.
    2. ```python
       RandomCrop(size, ... )
       ```
       랜덤한 위치에서 지정한 크기로 이미지를 자르는 함수.\
       size는 Resize랑 같은 형식
       ```python
       CenterCrop(size, ... )
       ```
       중심을 기준으로 지정한 크기로 이미지를 자르는 함수.\
       size는 Resize랑 같은 형식
    3. ```python
       RandomRotation(degrees, ... )
       ```
       입력한 범위의 임의 값만큼 이미지를 회전하는 함수.\
       degrees가 sequence면 (min, max)의 범위로 인식하고 정수면 (-degrees, degrees)의 범위로 인식.
    4. ```python
       RandomVerticalFlip()
       RandomHorizontalFlip()
       ```
       이미지 뒤집음
    5. ```python
       Compose("""list of transforms object""")
       ```
       여러 transform을 하나로 합쳐서 한번에 처리할 수 있게 함
    6. ```python
       ToTensor()
       ToPILImage()
       ```
       텐서를 이미지로 바꾸거나 텐서를 이미지로 바꾸는게 가능함