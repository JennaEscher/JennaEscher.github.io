---
title: "Python Library 1. matplotlib"
header:
  overlay_image: /assets/images/maxim-hopman-fiXLQXAhCfk-unsplash.jpg
  caption: "Photo By @Maxim Hopman On [**Unsplash**](https://unsplash.com/@nampoh)"
categories:
  - Computer Science
  - Python
tags:
  - Python Library
  - Matplotlib
excerpt: >
  파이썬의 다양한 라이브러리에 대해 공부해보자.<br />
use_math: true
---

## 1. matplotlib 소개

**matplotlib**는 주어진 데이터를 그래프나 차트로 시각화하는 것을 도와주는 Python의 라이브러리이다. 후술될 numpy, pandas 등의 라이브러리와 같이 쓰일 수 있다. 이 라이브러리는 Python의 내장 라이브러리가 아니기 때문에 **별도의 설치 과정**이 필요하다.
{: style="text-align: justify;"}

설치 과정은 간단하다. 명령 프롬프트(cmd)를 열고, `pip install matplotlib`를 입력하고 Enter 키를 누른다.
{: style="text-align: justify;"}

```
Microsoft Windows [Version 10.0.19043.1706]
(c) Microsoft Corporation. All rights reserved.

C:\Users\jenna>pip install matplotlib
```

필자는 이미 matplotlib가 설치되어 있기 때문에 아래 이미지와 같이 출력된다.
{: style="text-align: justify;"}

```
Microsoft Windows [Version 10.0.19043.1706]
(c) Microsoft Corporation. All rights reserved.

C:\Users\jenna>pip install matplotlib
Requirement already satisfied: matplotlib in c:\programdata\anaconda3\lib\site-packages (3.4.3)
Requirement already satisfied: pyparsing>=2.2.1 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (3.0.4)
Requirement already satisfied: pillow>=6.2.0 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (8.4.0)
Requirement already satisfied: python-dateutil>=2.7 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (2.8.2)
Requirement already satisfied: kiwisolver>=1.0.1 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (1.3.1)
Requirement already satisfied: numpy>=1.16 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (1.20.3)
Requirement already satisfied: cycler>=0.10 in c:\programdata\anaconda3\lib\site-packages (from matplotlib) (0.10.0)
Requirement already satisfied: six in c:\programdata\anaconda3\lib\site-packages (from cycler>=0.10->matplotlib) (1.16.0)

C:\Users\jenna>
```

설치한 matplotlib를 사용하고자 한다면, 반드시 `import matplotlib` 명령어를 이용해 먼저 라이브러리를 **import**해야 한다.
{: style="text-align: justify;"}

## 2. matplotlib 활용

matplotlib 튜토리얼: [https://wikidocs.net/book/5011](https://wikidocs.net/book/5011)
{: style="text-align: justify;"}

위의 링크에 matplotlib 라이브러리에 대한 자세한 설명이 있다. 여기서는 자주 쓰이는 함수만 간단하게 설명하고자 한다. 지금부터 설명할 예제는 **Jupyter Notebook** 혹은 **Google Collab** 환경에서 실행하는 것을 추천한다.
{: style="text-align: justify;"}

```python
import matplotlib.pyplot as plt

plt.plot([0, 1, 4, 10])
plt.show()
```

<figure style="width: 500px" class="align-center">
  <img src="/assets/images/matplotlib_1.png" alt="">
</figure>

위의 코드는 단순한 꺾은선 그래프를 그린다. `plt.plot([0, 1, 4, 10])`와 같이 리스트 혹은 튜플, 후술될 Numpy Array의 형태로 값을 입력하면 Y 값으로 인식해 그래프를 그린다. 따로 명시된 바가 없으면 X 값은 기본적으로 **[0, 1, 2, 3]**이 되어 (0, 0), (1, 1), (2, 4), (3, 10)을 잇는 그래프가 나타난다.
{: style="text-align: justify;"}

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4], [0, 1, 4, 10])
plt.show()
```

위의 경우 전자는 X 값, 후자는 Y 값을 의미한다.
{: style="text-align: justify;"}

matplotlib를 통해 그리는 그래프는 선의 종류와 색상도 지정할 수 있다. 아래 예제를 살펴보자.
{: style="text-align: justify;"}

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [4, 4, 4], '-', color='lightcoral', label='Solid')
plt.plot([1, 2, 3], [3, 3, 3], '--', color='gold', label='Dashed')
plt.plot([1, 2, 3], [2, 2, 2], ':', color='forestgreen', label='Dotted')
plt.plot([1, 2, 3], [1, 1, 1], '-.', color='deepskyblue', label='Dash-dot')
plt.xlabel('X-Axis')
plt.ylabel('Y-Axis')
plt.axis([0.8, 3.2, 0.5, 5.0])
plt.legend(loc='upper right', ncol=4)
plt.show()
```

<figure style="width: 500px" class="align-center">
  <img src="/assets/images/matplotlib_2.png" alt="">
</figure>

코드를 차근차근 살펴보자.<br><br>`'-'`는 그래프의 선의 **종류**, `color='rgb_color'`는 선의 **색상**, `label='line_type'`은 **범례에 표시될 내용**을 의미한다. `plt.xlabel('X-Axis')`과 `plt.ylabel('Y-Axis')`에는 각 축의 **레이블**을 입력할 수 있다. `plt.axis([x_min, x_max, y_min, y_max])`는 **X, Y 축의 범위**를 지정한다. 마지막으로 `plt.legend(loc='upper right', ncol=4)`은 **범례**를 나타내는데, 여기서 `loc`는 **범례의 위치**, `ncol`은 범례의 **열 개수**를 뜻한다.
{: style="text-align: justify;"}

선으로 된 그래프 위에는 마커를 지정할 수 있다.
{: style="text-align: justify;"}
