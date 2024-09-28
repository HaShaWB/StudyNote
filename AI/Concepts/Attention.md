- 하나의 $X$ 를 Query, Key, Value로 나눠서 계산함
- Query, Key, Value 이름 자체는 특별한 이유는 없음
## Scaled Dot-Product Attention
- Input $X$를 선형변환 해 $K, \; V, \; Q$를 구하고, 이를 바탕으로 연산함
1. Input $X$: 주어진 input seqeunce를 쌓은 행렬
$$
X = [x_1,x_2,x_3, ... , x_n]^T \;\;\;\; where \;x_i:= embedded\;vector
$$
2. $Q, K, V$ : $X$를 선형변환해서 얻은 행렬 ($d_k$ := $K$의 각 벡터의 차원 ($K \in R^{n\times d_k}$  ))
$$
\begin{cases}
Q &= XW_Q \\
K &= XW_K\\
V &= XW_V
\end{cases}
$$
3. **Attention** : $Q, K, V$를 합치는 연산 ($\sqrt{d_k}$: Scale Factor)
$$
Attention(Q, K, V) = softmax(QK^T/\sqrt{d_k})V
$$

## Multi-Head Attention
- 여러 dot-product attention을 concate해서 구성한 레이어
1. 하나의 $(Q, K, V)$ 쌍에 대해, 서로 다른 선형변환을 해 $(Q_i, K_i, V_i)$를 계산
$$
\begin{cases}
Q_i &= QW_i^Q \\
K_i &= KW_i^K\\
V_i &= VW_i^V
\end{cases}
$$
2. 각각의  $(Q_i, K_i, V_i)$ 쌍에 대한 head를 계산
$$
head_i = Attention(Q_i, K_i, V_i)
$$
3. 모든 head를 합치고 선형변환
$$
MultiHead(Q, K, V) = concate(\forall head_i) W^O
$$
