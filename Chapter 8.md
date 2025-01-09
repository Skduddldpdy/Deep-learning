## 8-1
- DNN을 무턱대고 깊게 만들면 Vanishing gradient, Overfitting, loss landscape가 꼬불해진다는 문제 발생
1. Vanishing
   > - layer가 많으면 입력 층에 가까울수록 미분이 사라짐
   > - 주범은 sigmoid (최대 기울기 1/4), 앞에서 입력 데이터를 망쳐놓으면 뒤에서 손 쓸 방법이 없다
   > - gradient 소멸 -> update x -> 앞단에 이상한 weight -> 깊은게 오히려 독이 됨
   > - ReLU, Batch Normalization, Layer Normalization으로 해결
- ReLU (Rectified Linear Unit)
  > ![image](https://github.com/user-attachments/assets/3bb40140-4723-41de-b396-06e24e5d0b82)
  > 1. Leaky ReLU : 음수 부분 y=0.01x
  > 2. Parameter ReLU : 음수 부분 y= ax (기울기 미분 -> 액웨액웨..들어가는 값으로 끝남)
  > - 항상 ReLU가 Sigmoid보다 Vanishing 해결? NO, 노드의 수가 많을 때만 (양수 확실히 살리고 음수 확실히 죽임)
## 8-2
- Batch Normalization 배치 정규화 <br>
  : 어디로 이동시킬지를 학습, 어디에(평균) 얼만틈 세게 뿌릴지(분산)를 학습 <br>
  : 해당 node에 대해 nonliearity를 얼마나 살리면서 vanishing gradient을 얼마나 해결할지 AI가 알아내는 것
  > - Batch size 들어가는 값을 적절하게 들어가도록 순서는 유지하되 재배치
  > - 평균 0 분산 1 이 되도록 재배치(normalization)
  > - $a \left( \frac{X - \overline{X}}{\sigma x} \right) + b$ => 어디에(평균 b), 얼만큼 퍼지게(분산 $a^2$)
  > - 주로 activation 전에 이 행위를 할 layer의 각 node에 BN을 추가하는 식으로 적용
  > - Training 때와 Test 때 다르게 적용 -> 학습 때 쭉 저장해온 값을 Test 때 사용
  > - 단점 : Batch size에 따라 영향을 받음
  > - 이미지 데이터 작업에서 주로 사용
- Layer Normalization 레이어 정규화
  > ![image](https://github.com/user-attachments/assets/1d09c308-d7a3-4022-bceb-8db25f416de1)
  > - 노란색으로 표현된 각 노드에 해당하는 값을 이용해 평균과 분산 계산
  > - Training 때와 Test 때 똑같은 방식으로 계산
  > - 장점 : Batch size에 영향을 받지 않음
  > - 자연어 처리에서 주로 사용 (pad 토큰 때문에)
## 8-3 
2. Loss landscape가 꼬불해지는 문제
   > - 깊게 만들수록 loss 모양이 이상해짐
   > - ResNet의 skip-connection이 대표적인 해결 방안 중 하나
   >> : Skip Connection이란 신경망의 한 층 또는 여러 층의 출력을 다음 층의 입력에 직접 더하는 연결
## 8-4,5,6
3. Overfitting 과적합
   : Training 땐 잘하는 데 Test 때 못하는 것
   > - 모델 경량화 : 입력과 출력 간의 관계를 복잡하게 하지 말고 모델을 단순하게 만들음
   > - data augumentation, Dropout, Regularization 등으로 해결
- data augumentation 데이터 증강
  > - 데이터를 더 구하기 힘드면 자르고, 돌리거나 찌부시키는 등 다양하게 우려먹어서 데이터 증가
- Drop out <br>
  : 랜덤하게 노드 가려보면서 학습
  > - 적용시키고 싶은 layer에 dropout 적용, 살릴 확률 p는 hyperparameter
  > - 네트워크에 통과 시킬 때마다 살릴 노드 다시 고름 (데이터 마다 다시 정함)
  > - test 땐 전원 살림
  > - 노드가 필요 이상으로 많다면 -> loss를 잘 줄이지만 기계적으로 정답을 맞힐 뿐 -> overfitting -> dropout -> 각 노드가 의미 있는 특징을 뽑음
- Regularization <br>
  : loss에 weight의 크기를 더해서 같이 고려하려 함
  > - $L$ 대신 $L + \lambda \| \mathbf{w} \|_p^p$를 loss로 사용
  >>  p가 1이면 l1-regularization, p가 2면 l2-regularization
  >> ![image](https://github.com/user-attachments/assets/50fd956d-06bd-4bce-acff-98f870c4f98b)
  > - weight를 줄이려고 하는 이유
  >> 1. loss 줄이는 데 별 영향 없는 weight는 0으로 => 모델 경량화 (큰 weight는 더 복잡한 모델을 의미)
  >> 2. 어느정도 수렴하고 나서도 계속 학습시켜보니 weight가 자꾸 커짐
  > - 처음엔 L을 많이 고려하다가 L을 어느정도 줄였으면 L이 도로 너무 커지지 않는 선에서 lp(p값)를 줄임
  > - weight 크기도 같이 고려해 쓸데없이 큰 애들 망치로 두듣겨 줌
  >> 1. l1 : 기울기가 일정 -> 크건 작건 똑같은 힘드로 두드림 -> 몇개 connection을 없대는 효과 (중요한 것만 살림)
  >> 2. l2 : weight가 작은 애들은 살살 때리고, 큰 애들은 팍팍 때림
  > - 수학적으로는 MAP (Maximum A Posteriori)로 해석
  >> - likelihood만 고려하던 것에서 prior distribution까지 고려하는 것으로 <br>
  >> 1. l1이면 라틀라시안을 prior distribution
  >> 2. l2면 가우시안을 prior distribution




