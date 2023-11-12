<h3>강의 목차</h3>

1. Introduction to NLP Task
2. Word Embedding
3. RNN, LSTM, GRU
4. Seq2Seq with attention
5. Beam Search
6. Metric


<h2>NLP</h2>

- NLU: Understanding
- NLG: Generation

<h3>Bag of Words</h3>

- 단어의 빈도수 만으로 문장 구분
1. 문장의 고유한 단어를 Vocabulary set을 만들고
2. one-hot vector의 합으로 나타냄

처음보는 단어가 나오면 확률을 0으로 계산해버림

<h3>Word Embedding</h3>
- Word2Vec
  > 단어를 다른 단어와의 관계를 고려하여 벡터공간에 배치
  - $W_2W_1x$ 로 Input에서 원하는 Output이 나오도록 학습

- GloVe
  - 단어가 동시에 등장할 확률을 기반으로 관련성 학습

<h3>RNN</h3>

> Recurrent Neural Networks

$\begin{align*}x_t\rarr&\text{RNN}\rarr h_t\\ &\darr\\x_{t+1}\rarr&\text{RNN}\rarr h_{t+1}\end{align*}$
$h_t=f_t(h_{t-1},x_t)$

종류
- one to one
- one to many
- many to one
- many to many

단점
 - Gradient vanishing
 
Solution
  - LSTM

    Cell state에 정보를 저장하여
    
    forget gate: 어느정도 비율만 남길 것인디
    
    input gate: 얼마만큼 반영할 것인지

    update gate: forget과 input gate에서 계산한 값을 합해서 $C_t$로 업데이트

    output gate: cell state로부터 출력할 정보 계산하고 출력
  
  - GRU

    cell state 없애고 hidden state로 대신함 $\rarr$ 경량화


<h3>Seq2Seq</h3>

인코더 + 디코더 구조; 문자열로 문자열을 만드는 모델


- Teacher Forcing: 수렴속도 빨라지지만 일반화성능 낮아짐
  - 학습 초반부에서만 사용


<h3>Beam Search</h3>

> 시퀀스 예측 작업에서 사용되는 휴리스틱 알고리즘

<h3>Metric</h3>

- F-measure:

    $\text{precision}=\frac{|\text{correct word}|}{\text{length of prediction}}\\\text{recall}=\frac{|\text{correct word}|}{\text{length of prediction}}\\$

    - 순서가 달라도 reference에 있다면 100%가 나올 수도 있음

- BLEU
  > Bilingual Evaluation Understudy

  - 단어를 2, 3, 4 개씩 묶은 부분문자열로 precision 구하고 이들의 기하평균에 brevity penalty를 곱하여 BLEU 계산
    - brevity penalty: 길이에 따른 페널티 $\frac{|\text{predict}|}{\text{reference}}$