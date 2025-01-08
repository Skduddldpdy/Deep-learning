## 6-1
- non-linear activation으로 이진 분류
  > 입력 : 키와 몸무게 & 출력 : 1(살 빼야 하는 사람) or 0(살 쪄야 하는 사람) <br>
  > step1. 데이터 모으기 <br>
  > step2. 모델 만들기 : unit step fuction 이용해 분류, 입력 노드 2개 출력 노드 1개, hidden layer 없으면 퍼셉트론이라고 함 <br>
  > step3. 모델 학습 시키기 : 분류 경계가 선형이 되면 선형 분류
  > step4. 모델 테스트하기 : 3D로 표현되는 것 확인, 입려과 출력과의 관계는 비선형 <br>
  > 한계점 : 미분 불가, 너무 빡빡하게 분류 => sigmoid로 해결 가능
- sigmoid
  > - 전구간 미분 가능, 좀 더 부드러운 분류 가능
  > - 확률(혹은 정도)로 해석 가능
  > - 가장 멀리 찢어 놓는 합리적인 분류 경계 선 찾게 됨
## 6-2,3
- sigmoid를 이용한 이진 분류
  > - 입력은 3*100*100인 (강or고) 사진이며 바로 출력 층으로 연결된다고 가정 <br>
  > - 파라미터 30001개 -> gradient길이 30001 -> Loss 정의 => BCE Loss (이진분류에 적합)
  > - 신경망이 사진을 입력 받아 강아지일 확률 출력 -> 강아지 사진을 넣었을 때 0에 가까운 값이 나올수록 Loss가 커지도록 함 <br>
  > - **Loss로 "출력의 의미" 컨트롤** <br>
  > - If 강아지 maximize q(신경망 출력), IF 고양이 maximize (1-q) => $q^y (1-q)^{1-y}$
- BCE (Binary Cross Entropy)
  > - 여러 데이터에 대한 예측 확률 모두 곱함 -> Underflow 문제 막기 위해 log -> 음수를 취하고 평균으로 구함
  > - MSE보다 훨씬 더 오차에 민감함
  > - Loss fuction 개형이 MSE는 non-convex이지만 BCE는 convex(아래로 볼록)이다 -> local이 global 값
  > - $\text{BCE Loss} = - \frac{1}{N} \sum_{i=1}^N \left[ y_i \cdot \log(\hat{y}_i) + (1 - y_i) \cdot \log(1 - \hat{y}_i) \right]$
- Logistic Regression
  > : 입력과 출력 사이의 관계를 확률 함수로 표현하고 이 함수를 은닉층이 없는 인공 신경망으로 놓고 추정하는 방법 (위와 같은 예제) <br>
  > + 분류 문제를 다루는데도 '회귀'라고 하는 이유는 분류와 회귀가 근본적으로 같은 접근 방식 공유하기 때문
## 6-4
- MLE (Maximum Likelihood Estimation) <br>
  : Loss를 최소화하는 파라미터를 찾는 딥러닝의 학습 과정 <br>
   즉, 관측된 Measurement가 나올 가능성을 최대로 하는 파라미터 찾는 과정 
  > - BCE Loss와 MSE Loss 모두 Likelihood라는 공통된 뿌리이지만 가정한 분포가 다름 <br>
  >> - Likelihood <br>
  >>  : 앞의 것을 보고 그 속에 숨겨져 있는 뒤에 것을 알아낸다 (조건부 확률 값이지미나 확률분포는 아님, 합 != 1
  > - BCE : 베르누이로 가정하고, 신경망이 'y1 = 1일 확률 q1'을 잘 출력하게끔 NLL을 loss로 삼고 학습
  > - MSE : 가루시안로 가정하고, 신경망이 '랜덤변수 y1의 평균'을 y1과 가깝게 나오도록 NLL을 loss로 삼고 학습
  >> BCE-베르누이 / MSE-가루시안 / MAE-라플라시안 / CE-멀티누이
## 6-5
- 다중분류
  > - 입력이 3*100*100인 (강or고or소) 사진이라면 확률 3개가 필요
  > - 파라미터 90003개 -> 그라디언트 길이 90003
  > - 출력 노드의 수를 늘려서 각 노드가 각 동물을 담당하도록 정답(label) y는 강[1:0:0] 고[0:1:0] 소[0:0:1] => **ont-hot encoding**
  > - 확률 분포가 출력되도록 마지막 액티베이션은 softmax 사용
  > - MLE로 생각하면 멀티누이(또는 카테고리컬) 분포를 따를 것이다
  > - ont-hot 고려하면 0 <= -logq 즉, 한놈만 팬다 (하나 1로하면 나머지 자동으로 0)
- Softmax
  : 여러 개의 실숫값을 입력받아 각 출력의 값이 양수이면서 그 합이 1이 되도록 변환하는 함수
  > ![image](https://github.com/user-attachments/assets/123b09df-8083-4f71-8174-acf225c7379c)
- CE(Cross Entropy Loss)
  > : 레이블이 카테고리분포(멀티누이)를 따른다고 가정하고 NLL을 구하며 이를 통해 얻은 Loss
  > - $\text{Cross-Entropy Loss} = - \sum_{i=1}^N y_i \log(\hat{y}_i)$
  > - 항상 엔트로피보다 크거나 같음
  > - CE를 줄일수록 머신의 출력이 label과 가까워짐
- 정리
  > step1. 입,출력 정의 (회귀, 다중분류, multi-label) <br>
  > step2. model 만들기 (MLP, CNN, RNN) <br>
  > step3. Loss 정의 (회귀-MSE, 이진-BCE, 다중-CE, 사실은 다 NLL) <br>
  > step4. weights 최적화 (SGD, Adam) 
 

