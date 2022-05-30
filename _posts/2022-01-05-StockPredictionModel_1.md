---
title: "Stock Prediction Model 1. LSTM"
header:
  overlay_image: /assets/images/ilya-pavlov-OqtafYT5kTw-unsplash.jpg
  caption: "Photo By @Ilya Pavlov On [**Unsplash**](https://unsplash.com/@ilyapavlov)"
categories:
  - Project
  - Economics
  - Computer Science
tags:
  - LSTM
  - Time Series
  - Stock Market
excerpt: >
  주가 예측 모델에 대해 공부해보자.<br />
use_math: true
---

2022년 새로운 프로젝트를 진행하기에 앞서, Time Series Analysis에 대한 기초 지식을 다시 한 번 짚고 넘어가야겠다는 생각이 들었다. 따라서 [huseinzol05/Stock-Prediction-Models](https://github.com/huseinzol05/Stock-Prediction-Models)의 코드를 참고한 뒤 본격적으로 주제를 정해 프로젝트를 진행하고자 한다.
{: style="text-align: justify;"}

필자는 학부생이며 아래의 개념 정리는 순전히 본인의 이해를 돕기 위한 것이기 때문에 부정확하거나 모호한 정보가 포함되어 있을 수 있다는 점을 참고하기 바란다.
{: style="text-align: justify;"}

## 1. LSTM의 개념

**RNN**(순환신경망, Recurrent Neural Network)은 Neural Network의 일종으로 노드들의 레이어가 연속적으로 연결되어 있는 구조를 말한다. RNN에는 **Input** 노드와 **Output** 노드, 그리고 **Hidden** 노드 총 3가지 종류의 노드들이 존재한다.
{: style="text-align: justify;"}

<figure class="align-center">
  <img src="/assets/images/Recurrent_neural_network_unfold.png" alt="">
</figure>

위의 그림을 보면 RNN의 펼쳐진 구조를 확인할 수 있다. 초록색 원은 Input 노드, 빨간색 원은 Output 노드를 나타내고 가운데 서로 연결되어 있는 사각형이 Hidden 노드이다. 각 노드들 사이의 연결은 실수의 **가중치**를 가지고 있으며, 이 값은 바뀔 수 있다.
{: style="text-align: justify;"}

Input 노드($x_{t}$)로 입력값이 들어오면 $U$와 $V$, $h_{t-1}$의 값을 이용해 **비선형 함수**인 하이퍼볼릭 탄젠트 함수로 $h_{t}$의 값을 계산하게 된다. 이때 이 함수를 **활성 함수**라고 부른다. Output 노드($o_{t}$)로 출력되는 값을 구할 때에는 상황에 따라 Sigmoid 함수 혹은 Softmax 함수 등을 활용할 수 있다.
{: style="text-align: justify;"}

$U$와 $V$, $W$와 같은 가중치들은 하나의 층에서 값을 공유한다(Shared Weight). 하지만 층이 여러 개일 경우, 신경망의 학습이 진행됨에 따라 오차(신경망이 생성한 출력값과 정답에 해당하는 값 사이의 편차의 합)를 줄이는 방향으로 갱신되기 때문에 각 층 별 가중치는 동일하지 않다.
{: style="text-align: justify;"}

그러나 RNN은 노드 사이의 거리가 멀 수록 가중치에 따른 결과값의 기울기가 0에 가까워지는 **Vanishing Gradiants Problem**, 혹은 기울기 값이 계속 증폭되는 **Exploding Gradiants Problem**이 발생한다는 단점이 존재한다. 따라서 이를 보완한 것이 바로 **LSTM**(장단기 메모리, Long short-term memory)이다.
{: style="text-align: justify;"}

<figure class="align-center">
  <img src="/assets/images/LSTM_Cell.png" alt="">
</figure>

위 사진의 파란색 사각형은 RNN과 동일하게 Hidden 노드를 나타낸다. 그러나 이 Hidden 노드 안에는 **망각 게이트**(Forget Gate)가 추가되어, 위에서 언급되었던 RNN의 문제를 해결할 수 있다. 아래는 LSTM의 수식이다.
{: style="text-align: justify;"}

> $F_{t} = \sigma(W_{f}\cdot[h_{t-1}, x_{t}] + b_{f})$\\ > $I_{t} = \sigma(W_{i}\cdot[h_{t-1}, x_{t}] + b_{i})$\\ > $O_{t} = \sigma(W_{o}\cdot[h_{t-1}, x_{t}] + b_{o})$\\ > $c_{t} = F_{t} \odot c_{t-1} + I_{t} \odot tanh(W_{c}\cdot[h_{t-1}, x_{t}] + b_{c})$\\ > $h_{t} = O_{t} \odot tanh(c_{t})$
> {: style="text-align: justify;"}

## 2. 코드 분석

코드의 출처는 문서의 앞부분에 있으니 자세한 내용을 확인하고 싶은 사람은 위의 링크를 참고하면 된다.
{: style="text-align: justify;"}

```python
import sys
import warnings
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
from datetime import datetime
from datetime import timedelta
from tqdm import tqdm

if not sys.warnoptions:
    warnings.simplefilter('ignore')
sns.set()
tf.compat.v1.random.set_random_seed(1234)
```

라이브러리
{: style="text-align: justify;"}

```python
df = pd.read_csv('../Data/GOOG-year.csv')
df.head()
```
