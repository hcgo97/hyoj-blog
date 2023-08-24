---
title: LeetCode) Best Time to Buy and Sell Stock 2 알고리즘 문제
slug: "/LeetCode)-Best-Time-to-Buy-and-Sell-Stock-2-알고리즘-문제"
date: 2023-08-25
tags:
  - Algorithm
  - CodingTest
---

## 122. Best Time to Buy and Sell Stock 2 (주식을 사고 팔기 가장 좋은 시기 2)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0122-best-time-to-buy-and-sell-stock-ii](https://github.com/hcgo97/leetcode/tree/master/0122-best-time-to-buy-and-sell-stock-ii)_
- _링크: [https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)_

> ### 문제 설명
>
> 정수 배열 가격이 주어지는데, 여기서 가격`[i]`은 해당 날짜의 주식 가격입니다.
>
> 매일 주식을 매수 및/또는 매도할 수 있습니다. 한 번에 최대 한 종목의 주식만 보유할 수 있습니다. 그러나 매수한 후 같은 날 즉시 매도할 수 있습니다.
>
> 달성할 수 있는 최대 수익을 찾아서 반환하세요.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `prices = [7,1,5,3,6,4]`
>
> - **Output:**
>   - `7`
>  
> - **Explanation:**
>   - 2일차에 매수(`price = 1`)하고 3일차에 매도(`price = 5`), 수익 = `5-1` = `4`.
>   - 그런 다음 4일째에 매수(`price = 3`)하고 5일째에 매도(`price = 6`)하면 수익 = `6-3` = `3`이 됩니다.
>   - 총 수익은 `4 + 3` = `7`입니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `prices = [1,2,3,4,5]`
> 
> - **Output:**
>   - `4`
>  
> - **Explanation:**
>   - 1일차에 매수(`price = 1`)하고 5일차에 매도(`price = 5`)하면 수익 = `5-1` = `4`가 됩니다.
>   - 총 수익은 `4`입니다.
>  
> ### **Example 3:**
> 
> - **Input:**
>   - `prices = [7,6,4,3,1]`
> 
> - **Output:**
>   - `0`
>  
> - **Explanation:**
>   - 플러스 수익을 낼 수 있는 방법이 없으므로 최대 수익 `0`을 달성하기 위해 주식을 매수하지 않습니다.
> 
> ### **Constraints:**
>
> - `1 <= prices.length <= 3 * 10^4`
> - `0 <= prices[i] <= 10^4`
>
<br></br>

## 풀이 과정

1. `prices` 배열이 2개 미만일 경우 `return 0` 처리 후 로직을 종료한다.
    ```python
    if len(prices) < 2:
        return 0
    ```
    
2. 이익 변수를 초기화 한다.
    ```python
    profit = 0
    ```

3. `prices` 요소 갯수 반복하는 `for-in` 문을 선언한다.
    ```python
    for i in range(1, len(prices)):
    ```

4. 현재 가격이 이전 가격보다 높을때만 이익을 업데이트하는 조건문을 작성한다.
    ```python
        if prices[i] > prices[i-1]:
            profit += prices[i] - prices[i-1]
    ```

5. `for-in` 문이 종료되면 이익을 `return` 한다.
    ```python
    return profit
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def maxProfit(self, prices):
        
        # 1. prices 배열 요소가 2개 미만일 경우 바로 return 0
        if len(prices) < 2:
            return 0
        
        # 2. 이익 변수 초기화
        profit = 0
        
        for i in range(1, len(prices)):
            # 3. 현재 가격이 이전 가격 보다 높을때만 이익이 나므로 이익을 업데이트함
            if prices[i] > prices[i-1]:
                profit += prices[i] - prices[i-1]
                
        return profit
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n)`
- `prices` 배열을 한 번 순회하므로 `O(n)` 의 시간 복잡도를 가진다.

### 공간 복잡도: `O(1)`
- `prices` 배열을 한 번 순회하고, 추가적인 배열을 사용하지 않으므로 `O(1)` 의 공간 복잡도를 가진다.
<br></br>


## 문제 풀이 기록
![hyoj leet code submit history](img1.png "hyoj leet code submit history")

<br></br>

## 다른 풀이 방법

### profit 배열을 활용한 방법 (시간: `O(n)`, 공간: `O(n)`)
- _*링크:* https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/discuss/590168/Easy-python-solution-faster-than-98.39)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
	# 1. prices 배열 요소가 1개 밖에 없으면 return 0
        if len(prices) < 2:
            return 0

	# 2. profit 배열 초기화
        profit = []

        for i in range(1, len(prices)):
	    # 3. 현재 가격과 이전 가격 차이를 계산해서 0보다 높은 경우(음수가 아닐때)에만 profit 배열에 추가
            profit.append(max(0, prices[i] - prices[i-1]))

	# 4. profit 배열 요소를 모두 합친 값을 return
        return sum(profit)
```