## 8-1
- DNN을 무턱대고 깊게 만들면 Vanishing gradient, Overfitting, loss landscape가 꼬불해진다는 문제 발생
1. Vanishing
   > - layer가 많으면 입력 층에 가까울수록 미분이 사라짐
   > - 주범은 sigmoid (최대 기울기 1/4), 앞에서 입력 데이터를 망쳐놓으면 뒤에서 손 쓸 방법이 없다
   > - gradient 소멸 -> update x -> 앞단에 이상한 weight -> 깊은게 오히려 독이 됨
- ReLU (Rectified Linear Unit)
  > ![image](https://github.com/user-attachments/assets/3bb40140-4723-41de-b396-06e24e5d0b82)
  > 1. Leaky ReLU : 음수 부분 y=0.01x
  > 2. Parameter ReLU : 음수 부분 y= ax (기울기 미분 -> 액웨액웨..들어가는 값으로 끝남)
  > - 항상 ReLU가 Sigmoid보다 Vanishing 해결? NO, 노드의 수가 많을 때만 (살리는 놈만 확실히 살리고 죽일 놈 확실히 죽임)

