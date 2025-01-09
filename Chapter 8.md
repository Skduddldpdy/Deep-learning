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


