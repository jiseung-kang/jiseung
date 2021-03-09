---
description: '풀이시간:30분,  시간 제한:1초, 메모리 제한:128MB'
---

# Greedy Algorithm\(1\)

## 큰 수의 법칙

다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙. 단, 배열의 특정한 인덱스\(번호\)에 해당하는 수가 연속해서 K번을 초과하여 더해질 수 없다. 서로 다른 인덱스에 해당하는 수가 같은 경우에도 서로 다른 것으로 간주한다.

* 배열의 크기 N, 숫자가 더해지는 횟수 M, 그리고 K가 주어진다. 
* 첫째 줄에 N\(2  &lt;= N &lt;= 1,000\), M\(1 &lt;= M &lt;= 10,000\), K\(1&lt;=K&lt;=10,000\)의 자연수가 주어지며,  각 자연수는 공백으로 구분한다. 
* 둘째 줄에 N개의 자연수가 주어진다. 각 자연수는 공백으로 구분하며 1 이상 10,000이하의 수로 주어진다. 
* 입력으로 주어지는 K는 항상 M보다 작거나 같다.

## How?

1. 가장 큰 수와 두 번째로 큰 수로 정렬해서
2. 가장 큰 수를 K번 더하고 두 번째로 큰 수를 한 번 더하는 연산을
3. 반복한다.

```text
# N, M, K를 공백으로 구분하여 받
n, m, k = map(int, input().split())

data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

result = 0

while True:
	for i in range(k):
		if m == 0:
			break
		result += first
		m -= 1
	if m == 0:
		break
	result += second
	m -= 1

print(result)
```

> Python 입출력  
> 여러 데이터를 한꺼번에 입력 받을 때 list\(\), map\(\)이용하기  
> map\(데이터타입, 입출력함수\)  
> list\(값\)

## Think

M의 크기가 커지면 시간 초과  
더 효율적으로 해결해보자

* 특정한 수열 형태로 일정하게 반복해서 더해지는 특징
* 반복되는 수열의 길이는 \(K + 1\)
* 수열이 반복되는 횟수 : M / \(K+1\)
* 가장 큰 수가 등장하는 횟수 : M / \(K+1\) \* K + M % \(K+1\) \#몫 + 나머지

```text
n, m, k = map(int, input().split())

data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

result = 0

count = int(m / (k+1)) * k
count += m % (k+1)

result += (count) * first
result += (m-count) * second

print(result)
```

