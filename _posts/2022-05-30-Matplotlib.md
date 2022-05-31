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

<figure class="align-center">
  <img src="/assets/images/matplotlib_1.png" alt="">
</figure>

위의 코드는 단순한 꺾은선 그래프를 그린다. `plt.plot([0, 1, 4, 10])`와 같이 리스트 혹은 튜플, 후술될 Numpy Array의 형태로 값을 입력하면 Y 값으로 인식해 그래프를 그린다. 따로 명시된 바가 없으면 X 값은 기본적으로 `[0, 1, 2, 3]`이 되어 (0, 0), (1, 1), (2, 4), (3, 10)을 잇는 그래프가 나타난다.
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
plt.title('Graph Title')
plt.show()
```

<figure class="align-center">
  <img src="/assets/images/matplotlib_2.png" alt="">
</figure>

코드를 차근차근 살펴보자.
{: style="text-align: justify;"}

- 선의 종류

| Linestyle | Name     | Description                                     |
| :-------: | -------- | ----------------------------------------------- |
|   `'-'`   | Solid    | 일반 실선 형태이다.                             |
|  `'--'`   | Dashed   | 긴 점선 형태이다.                               |
|   `':'`   | Dotted   | 짧은 점선 형태이다.                             |
|  `'-.'`   | Dash-Dot | 긴 점선과 짧은 점선이 번갈아 나타나는 형태이다. |

- 선의 색상

`plt.plot(color='color_name')` 방식으로 선의 **색상**을 지정할 수 있다. 'r', 'g', 'b', 'c', 'm', 'y', 'k', 'w' 와 같은 일반 색상부터 Tableau 색상, Hex Code, CSS 색상을 지원한다.
{: style="text-align: justify;"}

- 선의 Label

`plt.plot(label='label_name')` 방식으로 선의 **Label**을 지정할 수 있다. 지정된 Label은 추후에 설명될 범례에 표시된다.
{: style="text-align: justify;"}

- 축의 Label

`plt.xlabel('X-Axis')`, `plt.ylabel('Y-Axis')`로 표현할 수 있다. 괄호 안에 각 축에 붙일 Label명을 작성한다.
{: style="text-align: justify;"}

- 축의 범위

`plt.axis([x_min, x_max, y_min, y_max])` 로 표현할 수 있다. 각 **축의 범위**를 지정하는 역할을 한다.
{: style="text-align: justify;"}

- 범례

`plt.legend()` 방식으로 그래프의 범례를 표기할 지 정할 수 있다. 괄호 안에는 다양한 파라미터를 통해 세부 내용을 지정 가능하다. `loc` 파라미터는 범례의 **위치**, `ncol` 파라미터는 범례의 **열 개수**, `fontsize` 파라미터는 범례 **폰트의 크기**, `frameon` 파라미터는 범례 **테두리의 존재 유무**를 의미한다. 이 외에도 다양한 파라미터가 존재한다.
{: style="text-align: justify;"}

- 그래프 제목

`plt.title('Graph Title')` 방식으로 그래프 제목을 설정할 수 있다.
{: style="text-align: justify;"}

- 마커

선으로 된 그래프 위에는 마커를 지정할 수 있다. 아래 예제를 살펴보자.
{: style="text-align: justify;"}

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4], [2, 3, 5, 10], 'bo-')
plt.show()
```

<figure class="align-center">
  <img src="/assets/images/matplotlib_3.png" alt="">
</figure>

`'bo-'`에서 b는 색상, o는 마커의 종류, -는 선의 종류를 의미한다. 선의 종류와 색상은 위에서 언급된 것과 동일한 방식으로 작성하면 된다. 아래는 마커 중 일부를 나타낸 표이다.
{: style="text-align: justify;"}

| Marker | Name          | Description           |
| :----: | ------------- | --------------------- |
| `'o'`  | Circle        | 원형 마커             |
| `'s'`  | Square        | 사각형 마커           |
| `'v'`  | Triangle_Down | 아래 방향 삼각형 마커 |
| `'^'`  | Triangle_Up   | 위 방향 삼각형 마커   |

matplotlib를 통해 꺾은선 그래프 뿐만 아니라 다양한 형태의 그래프도 그릴 수 있다.
{: style="text-align: justify;"}

- 막대 그래프

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(3)
years = ['2018', '2019', '2020']
values = [100, 400, 900]

plt.bar(x, values)
plt.xticks(x, years)

plt.show()
```

<figure class="align-center">
  <img src="/assets/images/matplotlib_4.png" alt="">
</figure>

꺾은선/선형 그래프에서 사용하는 plt.plot() 함수와는 다르게, 막대 그래프를 그리기 위해서 **plt.bar()**라는 함수를 사용해야 한다. 이 함수의 사용법은 plt.plot()와 동일하다. 또 **plt.xticks()** 함수를 이용해 X 축에 **눈금을 설정**할 수 있다.
{: style="text-align: justify;"}

- 수평 막대 그래프

```python
import matplotlib.pyplot as plt
import numpy as np

y = np.arange(3)
years = ['2018', '2019', '2020']
values = [100, 400, 900]

plt.barh(y, values)
plt.yticks(y, years)

plt.show()
```

<figure class="align-center">
  <img src="/assets/images/matplotlib_5.png" alt="">
</figure>

- 산점도

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(0)

n = 50
x = np.random.rand(n)
y = np.random.rand(n)

plt.scatter(x, y)
plt.show()
```

<figure class="align-center">
  <img src="/assets/images/matplotlib_6.png" alt="">
</figure>

산점도란 두 변수의 상관관계를 좌표평면에 점으로 나타내는 그래프이다. 위의 코드를 살펴보면, 후술될 numpy 라이브러리의 rand 함수를 이용해 임의의 숫자를 x와 y에 각각 50개씩 배정을 했다. 그 후, **plt.scatter()** 함수를 사용해 도식화했다.
{: style="text-align: justify;"}
