## 1-1
1. 규칙기반 : 인간이 규칙을 만들음
2. 머신러닝 : 정답을 알려주면 AI가 규칙을 깨달음 
3. 딥러닝 : 깊은 인공신경망으로 스스로 학습
> - CNN(Convolutional Neural Network) : 이미지 데이터, 입력과 출력 모두 숫자
> - RNN(Recurrent Newral Network) : 연속적인 데이터, 입력과 출력 모두 숫자
---
## 1-2,3,4
1. 지도 학습 : 사람이 입력에 대한 정답을 미리 만들어 놓은 것 (회귀, 분류)
2. 비지도 학습 : 정답을 모름 (군집화, 차원 축소)
3. 자기지도 학습 : 진짜 풀려고 했던 문제 말고 새롭게 정의해서 먼저 풀어봄
> pretext task를 학습해서 pre-training <br>
> downstream task를 풀기위해 transfer learning 함
> - Context Prediction : 사전 학습 단계에서 이미지의 구조 및 객체 간 위치 관계를 학습하는 기법
>> 장점 : 레이블이 없는 데이터에도 적용 가능, 파란색 패치 위치를 임의로 선정할 수 있어 데이터 무한히 생성
> - Contrastive Learning : 이미지 간의 관계를 학습하는 자기 지도 학습 기법, 출처가 같다면 Attract, 출처가 다르면 Repel
>> 장점 : 가장 많이 사용 (GPT, BERT)
4. 강화 학습 
> - 용어 : Agent-행동 취하는 주체, Action-Agent가 취하는 행동, Reward-Action에 따라 받게되는 보상, Environment-강화 학습이 일어나는 무대(강아지 주인, 백돌), State-환경의 현재 상태, 행동 가치 함수 Q-State에서 Action을 했을 때 현재와 미래에 얻을 수 있는 Reward의 합의 기댓값, Episode-하나의 완전한 시행, Q_learning-Q값을 업데이트하여 최적의 행동 가치를 학습하는 방법, Exploration-기존에 학습하지 않은 새로운 방법을 찾는 것(𝜖-Greedy), Discount Factor r-Q값을 현재 시점으로 가져올 때 0~1사이 수를 곱해 좋고 나쁨 얘기해줌
