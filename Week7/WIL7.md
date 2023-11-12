## Bidirection RNN
### RNN의 문제점
- 과거 정보만 알 수 있고 미래의 정보는 알 수 없음
- 이를 해결하기 위해 뒤에서 시작하는 Backward RNN을 추가함
    - **한계점**
    - 순차적으로 정보를 처리하는 RNN 특성상 병렬처리 어려움
    - 멀리 떨어진 데이터가 도달하지 못하는 장기의존성 문제
    - 계산복잡도가 높음
## Transformer
- 모든 단어를 한번에 계산하므로 RNN같은 가진 순차적 계산이 필요 없음
- => 병렬처리에 유리함
- => 기울기 소실문제 해결
### Self Attention
- 입력 문장 내의 단어끼리의 연관성 추측
#### Scaled dot-product attension
- 세 가지 벡터를 계산: Query(Q), Key(K), Value(V)
- Query 벡터와 모든 Key 벡터 간의 내적을 계산해서 attenetion score계산
- K의 차원수의 제곱근으로 나누어 scailing 함
- 소프트맥스(softmax) 함수를 통해 가중치를 얻음
    - 모든 가중치는 0~1, 합은 1
- 이렇게 정규화된 점수들을 각각의 Value 벡터에 곱함
- Value를 합산하여 최종 출력을 생성
#### Positional encoding
- 입력(단어)가 한번에 들어와 순서정보를 알 수 없음
- 각 단어의 위치에 대한 정보를 단어의 벡터에 추가
- 같은 위치의 성분은 같은 값을 가져야하고 그 값이 너무 극단적이면 안되
    - sin, cos 함수의 주기를 1씩 늘려가면서 encoding을 함
#### Multihead Attention
- 다양한 관점에서의 정보를 포착하기 위해 Self attention을 여러개 만듦.
#### Masked Multihead Attention
- 현재위치 이후의 (미래의) 정보를 참조하지 못하도록 함

### GPT
> Genrative Pretrained Transformer
#### Generative
- 학습을 바탕으로 스스로 글을 생성
#### Pretrained
- 주어진 단어들 다음에 올 단어를 예측하는 학습을 함
- book corpus를 사용
#### Transformer
- Transformer Decoder 사용
- 학습과 같이 앞서 나온 내용만 참조할 수 있음

### BERT
> Bidirection Encoder Representaions from Transformers
- Masked language modeling task로 양방향의 문맥을 
- book corpus와 위키피디아를 학습
- task별로 최적의 learnig rate사용?