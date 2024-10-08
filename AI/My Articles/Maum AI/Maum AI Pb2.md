# Q2
```Plain Text
COIN [1] is a neural image compression model based on SIREN [2] architecture. 
It encodes pixel locations to RGB values by over-fitting an MLP.
A sample code of COIN and the model weights for one image(figure2e.png) are provided.
Given five similar images(figure2a∼figure2e), you need to modify the model to compress all images with a single model. 
The goal is to get five different images from the model. 
You should include image index(e.g. a : 0, b : 1, . . . ) in the input to specify which image to encode/decode.
```
### COIN의 이해
- 기본적으로 이미지를 모델로 '표상'하는 기법
	- 일반적인 '압축' 모델을 만드는 것이 아닌,
	- 이미지를 '표상'하는 모델을 만드는 것이 목표
- 일반적인 이미지를 압축하는 형태가 아니라, 특정한 이미지를 압축하는 것이 목적
	- 보통의 작업과 다르게 **과적합**이 주요 목표 중 하나
- Input=(x, y) -> Output=(R, G, B)
- 내부는 간단한 SIREN 레이어로 구성됨
- 이미지 복원은 단순히 각 (x, y)에 해당되는 RBG를 모와서 재구성
- 이미지가 *나름대로의* 규칙성이 있을 때 효과적일 것으로 예상됨
  => 랜덤 노이즈 같은 부분이 무시되기 쉬움
## Q2-1
```Plain Text
List possible modifications you can make to the model to achieve multiple image
compression.
```
'여러개의 이미지'를 어떻게 모델이 표상하도록 할 것인가.
특히, 이들을 어떻게 구분할 것인가.
#### 이미지의 좌표를 3차원으로 전환
- 기존에는 input으로 (x, y)를 넣었다면, input으로 (x, y, z=index)를 넣는 방식
- 제일 단순하며 깔끔한 방법
- 이미지 사이의 연관성 및 규칙성이 강할 수록 효과적일 것으로 *예상됨*
#### 이미지를 옆으로 잇는 방식
- 각 이미지의 너비를 w, 순서를 idx라고 할 때, 각 좌표를 다음으로 변환$$
Pos_i(x, y) = (x+idx*w, y)
$$
- 비슷한 방식으로 y방향으로 이을 수도 있음 -> 데이터의 형태에 따라 최적이 결정됨
- 이미지 사이의 연관성이 전혀 없을 때 효과적일 것으로 *예상됨*
- 특히, 이미지가 애매하게 닮은 경우 간섭 효과를 제거할 수 있지 않을까 *예상함*
#### Output을 조절하는 방식
- 기존의 input은 그대로 두고, output으로 rgb=(R, G, B)가 아닌 5개의 이미지의 rgb를 모두 담는 방식$$
RGBs = (*rgb_1, *rgb_2, \dots, *rgb_5)
$$
- 문제에서 input에 인덱스를 포함하라고 힌트를 줬지만, output을 바꾸겠다는 굳은 의지와 담대함의 결정체
- 5개의 이미지에 대해, 각 좌표의 rgb를 한번에 예측하는 방식
- 각 좌표에서, **5개의 이미지 사이의 연관성이 높을 때 특히 효과적**일 것으로 *예상함
- 또한, 모델의 이미지 간의 과적합을 최소화할 수 있는 방법으로 *예상됨*

## Q2-2
``` Plain Text
Choose one from the list and apply it. Submit the modified code, state_dict of
the model, the training log, and the reconstructed images.
```
- 채택한 방식: **Output을 조절하는 방식**
- 각 이미지가 음성 스펙토그램으로, 나름의 규칙성을 가지고 있음
- 특히 비슷한 음성에 대한 스펙토그램이기 때문에 규칙성이 매우 높음
- 또한, 모델의 과적합을 이용함과 동시에 이미지를 구분해야되기 때문에, 최적의 방식으로 *예상됨*
- 자세한 내용은 첨부된 파일 참고

## Q2-3
```Plain Text
Propose a metric to evaluate your model and evaluate it with the metric.
```
### 일반적인 방법
- (x, y) 좌표에 해당하는 Pixel에 대해, 실제 이미지의 픽셀과 모델이 예측한 픽셀의 RGB의 오차를 측정. 5개의 이미지에 대해 각각 계산함
	- ex: MSE, PSNR

### 모델 특화 Metric : 그래디언트 기반 에러
- 본 모델은 이미지를 재구성하는 것을 목표로 함
- 재구성된 이미지에서는 대체로 그 형상은 유사하나, 국소 범위 내에서의 급격한 변화가 뭉개지는 경향이 있음
- 극단적으로, 흰 바탕에 검은 점이 몇개 찍혀있는 이미지를 학습하면 *그냥 흰 바탕만 나올 가능성이 높음*
- 이러한 **국소 변화**를 잘 감지하기 위해서는, 단순히 이미지의 절댓값이 아닌, **이미지의 변화율**을 관찰할 필요가 있음
- 이를 위해 **GMSD(Gradient Magnitude Similarity Deviation)** 를 사용할 것을 제안함
- 이 방법은 **MSE**와 같은 기법과 같이 사용할 때 더욱 효과적임
#### GMSD
1. 이미지의 그래디언트를 계산 : Sobel 필터를 적용 $$
G = <G_x, G_y> \;\;\;\; G_x = S_x * I , \; G_y = S_y * I
$$
2. 각 이미지에 대해 그래디언트 맵을 구성$$
(G)_{ij} = ||G(i, j)||
$$
3. 두 이미지 사이의 그래디언트 유사도를 계산함 $$
S(\mathbf x) = \frac{2G_1(\mathbf x)G_2(\mathbf x) + C}{G_1(\mathbf x)^2 + G_2(\mathbf x)^2 + C} \;\;\;\; (C \sim 0)
$$
4. 각 픽셀에서의 유사도의 표준 편차를 계산함 -> 두 이미지가 **균일하게 비슷한지**를 확인$$
GMSD = std(S(\mathbf x))
$$

## Q2-4
``` Plain Text
Review the model architecture & results to see if there is any weakness
or limitation. Suggest further improvements to mitigate it if possible.
```
### 모델 리뷰
- 흔히 생각할 수 있는 이미지 압축 관련 AI 모델은 인코더-디코더 기반일텐데, 아에 모델 자체에 이미지를 주입한 형태가 매우 흥미로움
- 다만, 아이디어에 비해 모델 구조가 너무 단순해보임
- 물론, 모델이 복잡할 수록 모델 '압축'으로서의 의미가 약해지는 측면도 있음
- 그러나, 이미지의 특성을 조금 고려하면 더 좋은 방향으로 진화할 수 있을 것 같음
### 개선 방안 제안
#### 이미지 특화
- 주어진 이미지는 음성 스펙토그램으로, 임의의 이미지가 아닌, 특수한 형태의 이미지임
- 특히, 음성 스펙토그램의 가로축은 '시간'으로, 이는 이미지를 **시계열 데이터로 이해할 수 있음**을 의미함
- 또한, 음성의 세로축은 주파수로, 이 역시 물리적인 의미를 가짐
- 이 점을 고려했을 때, 모델 구조로 **RNN** 계열의 구조를 제안함
	- RNN 계열 중에서는 뭐가 효율적일지 실제로 해봐야 할 수 있음 (특히 '압축' 효율성 관점에)
#### RNN의 이점
- RNN은 시계열 데이터를 다루는데 매우 적합함
- 특히, Transformer와 같은 모델에 비해 최소 크기가 매우 작음
- 또한, 다음과 같은 방식으로 이미지를 구성하면 더욱 효율적인 압축이 가능할 것으로 *예상됨*
#### 이미지 복원(재구성) 방법
- 현재는 단순히 모든 좌표에 대한 RGB를 계산해서 이미지를 재구성함
- 이미지를 개별적으로 재구성하지 말고, **x 좌표에 따라서 재구성**하는 방법을 제안함
- 즉, 맨 처음에 **x=0**인 부분의 점들을 쭉 재구성함
- 이후, x 좌표가 같은 부분의 점들을 동시에 재구성함 -> x=n 라인을 따라서 재구성
- 이때, **x=n**인 부분의 점들을 예측할 때 **x=n-1**인 부분의 점의 데이터를 추가해줌
	- x=0에는 영벡터를 넣어줌
- 이런방식으로, 이전 이미지들까지 고려해서 다음 이미지를 예측할 수 있음
#### 최종 구조 제안
- input : $(x, \overline{RGB}s)$ => 이미지의 개수(5개)의 x좌표가 같은 각 line들의 RGB값
- output $\overline {RGB}s$
- 내부 구조 : RNN