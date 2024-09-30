- 모델의 [[Machine Learning#Predicted Value ($ mathbf y( mathbf x)$)|예측값]]과 [[Machine Learning#Target Vector ($ mathbf t$)|실젯값]]의 오차를 표현하는 함수

### Notaion
- $E$ : error function
	- $E(\mathbf w)$: 가중치가 $\mathbf w$일 때의 에러
- $x_i$ :[[Machine Learning#Input Vector ($ mathbf x$)|input vector]]
- $y$ : model
- $\mathbf w$ : model weight
- $t_i$ : [[Machine Learning#Target Vector ($ mathbf t$)|target vector]]
- $N$ : dim of [[Machine Learning#Target Vector ($ mathbf t$)|target vector]]

### Square Error
$$
E(\mathbf w) = \frac12 \sum\limits^N_{i} (y(x_i, \mathbf w) - t_i)^2
$$
### Root Mean Squre Error
$$
E_{RMS} = \sqrt{2E(\mathbf w^*)/N}
$$

- Add **Reularization**
	- $\mathbf w$의 크기를 억제해 overfitting을 방지
$$
\widetilde E_{RMS} = E_{RMS} + \frac \lambda 2 ||\mathbf w||^2
$$