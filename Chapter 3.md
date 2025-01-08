## 3-2
- 확률적 경사 하강법 SGD (Stochastic Gradient Descent) <br>
  : 랜덤하게 데이터 하나씩 뽑아서 loss 만듦, 하나만 보고 빠르게 방향 결정, 비복원추출, local minimum으로부터 탈출의 기회가 되기도, 불필요한 움직임이 많음
## 3-3
- mini-batch SGD
   : mini-batch size만큼 랜덤하게 데이터를 뽑아 loss 만듦
- GD의 느리다는 문제 GPU 해결 -> 병렬 연산 but 무작정 batch size 키우지말고 최대 8k까지만 because local minimum에 빠질 수도 있음
> batch size 커질수록 loss 커짐
> 1) learning rate도 같이 키우고 (Linear Scaling Rule: BS 두 배 하면 LR 두 배)
> 2) warm up (learning rate를 0부터 시작해 쭉 올려줌)도 해야 그나마 작은 batch size일 떄의 성능을 얻을 수 있기 때문
- 용어 정리
> Epoch:전체 데이터를 몇 번 반복 / Batch size:몇개씩 볼건지 / Learning rate:얼만큼 갈건지 => 이런 것들을 hyperparameter라고 함
> parameter : AI가 스스로 알아내는 변수 (weights, bias) vs hyperparameter : 내가 정해줘야 하는 변수 (Epoch, batch size, Initial weight, learning rate)
## 3-4
- "Gradient는 항상 등고선에 수직"
- Momentum : 그라디언트를 누적함으로써 관성을 가지게 함
  >![image](https://github.com/user-attachments/assets/ab1d0cea-0fda-4fd7-b704-6d81894c5784)
## 3-5
-RMSprop(Root Mean Square Propagation) : 그라디언트 크기만을 누적
> Learning rate를 각 파라미터 별로 다르게 준 셈(가파른 쪽은 조심 완만한 쪽은 과감) -> 평준화를 통해 공평하게 탐색
## 3-6
-Adam(Adaptive Moment Estimation) : 분자 momentum + 분모 RMSprop 반영, 이전 그라디언트는 잊어가면서 누적 
![image](https://github.com/user-attachments/assets/ac97ec40-86ea-40d7-8230-829ee1c76610)


