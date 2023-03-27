# 3주차
<br>
<br>

# 기본 알고리즘
<br>

### 알고리즘 문제를 푸는 큰축 (방법)

1. 분할 정복 알고리즘
2. Greedy 알고리즘

<br>

# 분할 정복(Divide-and-Conquer) 알고리즘

<img width="600" alt="image" src="Basic-algorithm-img/Untitled.png">
<br>
<br>

### Example

### 여러 개(N개)의 동전에서 저울을 이용하여 가짜 동전 찾기

- 최악의 경우 : N - 1 번째에 찾음

- 최선의 경우 : 한 번에 찾음!

$$
O(n)
$$

### 크기가 n인 입력을 2개로 분할하고, 각각 분할된 부분 문제의 크기가 n/2이라 하면,

<img width="450" alt="image" src="Basic-algorithm-img/Untitled 1.png">
<br>
<br>
### 크기가 n인 입력을 3개로 분할하고, 각각 분할된 부분 문제의 크기가 n/3이라 하면,

<img width="450" alt="image" src="Basic-algorithm-img/Untitled 2.png">
<br>
<br>

## 원하는 숫자 찾기

- 순차 탐색 `Sequential Search` : $O(n)$

- 숫자가 오름차순으로 정렬되어 있는 경우? → 반으로 나누어 찾기 : 분할 정복 알고리즘

<br>

## 분할 정복 알고리즘

- 주어진 문제의 입력을 분할하여 문제를 해결(정복)하는 방식의 알고리즘

- 분할한 입력에 대하여 동일한 알고리즘을 적용하여 해를 계산

- 이들의 해를 취합하여 원래 문제의 해를 얻음

- 분할된 입력에 대한 문제를 부분문제(sub problem)라고 함

- 부분문제는 **더 이상 분할할 수 없을 때까지** 계속 분할

- 부분 문제의 해를 **부분해**라고 함

<br>

## 정복 과정

- 대부분의 분할 정복 알고리즘은 문제의 입력을 단순히 **분할**만 해서는 해를 구할 수 없음

- **분할된 부분문제들을 정복 필요** → **부분해**를 찾아야 함

- 정복하는 방법은 문제에 따라 다르나, 일반적으로 부분 문제들의 해를 취합하여 보다 큰 부분 문제의 해를 구함

<br>
<br>


# 탐욕 알고리즘 Greedy Algorithm

## 욕심내어 풀어보자

- 문제를 해결하는 과정에서 항상 작은 것(문제에 따라서 가장 큰것)을 선택하는 방식으로 문제의 해를 구하는 것

- **입력 데이터 사이의 관계를 고려하지 않고** 수행과정에서 무조건 욕심내어 데이터를 선택

→ 근시안적 선택

- 탐욕 알고리즘은 지속적인 **근시안적인 선택을 모아서** 문제의 해를 얻음

- **일단 선택한 것에 대해 절대로 번복하지 않음**

- 이미 선택된 데이터를 버리고 다른 것을 선택하지 않음
    
    → 이러한 특성으로 대부분의 탐욕 알고리즘은 매우 단순
    
    → 반면에 제한적인 문제들만이 탐욕 알고리즘으로 해결