## 2-1
- 인공신경 : 노드와 엣지로 이루어져 웨이트 곱하고 바이어스와 함께 더해 액티베이션
![image](https://github.com/user-attachments/assets/32baa352-d9c5-4cc8-accd-ed6041cf1034)
> - Bias : 신경의 민감도 조절
> - Weight : 각 자극의 중요도 결정
- 인공신경망 : 인공신경의 반복
> FC(Fully Connected) layer : 노드끼리 싹 다 연결한 층 <br>
> MLP(Multilayer Perceptron) layer : 모든 layer가 FC layer인 신경망
---
## 2-2
- 인공신경망은 '함수'다 : 수 많은 데이터를 넣어서 "이 입력에는 이 출력이 나와야 돼"를 반복해 입력과 출력을 연결하는 함수를 알아 내 새로운 데이터에 대해서도 적절한 출력 (wight, bias 알아내는 것이 딥러닝의 목표)
---
## 2-3
- 선형회귀 : 입력과 출력 간의 관계를 선형으로 놓고 알아내는 것 (처음 보는 입력에 대해 적절한 출력을 얻기 위해)
> 최적의 웨이트, 바이어스를 알아내야 함 (선형회귀는 머신러닝에 해당) => loss를 최소화하는 a,b
> Loss 계산법
>> 1. MSE(Mean squared) Loss : 에러를 제곱하고 평균 -> 큰 오차, 이상치에 민감
>> 2. MAE(Mean Absolute Error) Loss : 절댓값을 취하고 평균 -> 큰 오차, 이상치에 둔감
> a,b를 일일이 바꿔가며 a,b찾는 것은 불가능 이를 경사하강법 해결
---
## 2-4 
- 경사하강법 : 아무렇게나 a,b 정하고 현재 위치에서 가장 가파르게 내려가는 방향으로 이동
> 단점 : 너무 신중하게 방향 선택 해 느림, local minimum에 빠질 수 있음
- Gradient : 항상 함숫값이 가장 가파르게 증가하는 방향, 현재위치에서 Gradient구한 후 그 반대 방향으로 이동 Gradient Descent
- Learning Rate : 그래디언트의 반대 방향으로 이동할 때 그 보폭을 조절하는 역할
---
## 2-5
-웨이트 초기화 기법 : 랜덤하게 0 근처로
![image](https://github.com/user-attachments/assets/2965a837-43af-4d3a-9345-900003296cd3)
