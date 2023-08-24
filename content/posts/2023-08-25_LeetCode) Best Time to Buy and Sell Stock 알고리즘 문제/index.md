---
title: LeetCode) Best Time to Buy and Sell Stock 알고리즘 문제
slug: "/LeetCode)-Best-Time-to-Buy-and-Sell-Stock-알고리즘-문제"
date: 2023-08-25
tags:
  - Algorithm
  - CodingTest
---

## 121. Best Time to Buy and Sell Stock (주식을 사고 팔기 가장 좋은 시기)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0121-best-time-to-buy-and-sell-stock](https://github.com/hcgo97/leetcode/tree/master/0121-best-time-to-buy-and-sell-stock)_
- _링크: [https://leetcode.com/problems/best-time-to-buy-and-sell-stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)_

> ### 문제 설명
>
> 가격 배열이 주어지는데, 가격`[i]`은 특정 주식의 째 날 가격입니다.
>
> 한 주식을 매수하기 위해 하루를 선택하고 해당 주식을 매도하기 위해 미래의 다른 날을 선택함으로써 수익을 극대화하고자 합니다.
>
> 이 거래에서 얻을 수 있는 최대 수익을 반환합니다. 수익을 얻을 수 없으면 `0`을 반환합니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `prices = [7,1,5,3,6,4]`
>
> - **Output:**
>   - `5`
>  
> - **Explanation:**
>   - 2일차에 매수(`price = 1`)하고 5일차에 매도(`price = 6`), 수익 = `6-1` = `5`입니다.
>   - 매도하기 전에 매수해야 하므로 2일차에 매수하고 1일차에 매도하는 것은 허용되지 않습니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `prices = [7,6,4,3,1]`
> 
> - **Output:**
>   - `0`
>  
> - **Explanation:**
>   - 이 경우 트랜잭션이 수행되지 않으며 최대 수익은 `0`입니다.
> 
> ### **Constraints:**
>
> - `1 <= prices.length <= 10^5`
> - `0 <= prices[i] <= 10^4`
>
<br></br>

## 풀이 과정

1. `prices` 배열이 비어있다면 `return 0` 처리 후 로직을 종료한다.
    ```python
    if len(prices) == 0:
        return 0
    ```
    
2. 이익 변수와 최소 가격 변수를 초기화 한다.
    ```python
    profit = 0
    min_price = prices[0]
    ```

3. `prices` 배열을 순회하는 `for-in` 문을 선언한다.
    ```python
    for price in prices:
    ```

4. 현재 가격이 최소 가격보다 낮으면 현재 가격을 최소 가격으로 설정하는 로직을 작성한다.
    ```python
        if price < min_price:
            min_price = price
    ```

5. 현재 가격에서 최소 가격을 뺀 값이 기존 이익보다 높으면 이익 변수를 업데이트하는 로직을 작성한다.
    ```python
        else:
            profit = max(price - min_price, profit)
    ```

6. `for-in` 문이 종료되면 이익을 `return` 한다.
    ```python
    return profit
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def maxProfit(self, prices):
        
        # 1. prices 배열이 비어있다면 return 0
        if len(prices) == 0:
            return 0
    
        # 2. 이익 변수 초기화
        profit = 0
        
        # 3. 최소 가격 변수 초기화
        min_price = prices[0]
        
        for price in prices:
            
            # 4. 현재 가격이 최소 가격보다 낮으면 현재 가격을 최소 가격으로 설정
            if price < min_price:
                min_price = price
                
            else:
                # 5. 현재가격 - 최소가격 뺀값이 기존 이익보다 높으면 이익을 업데이트
                profit = max(price - min_price, profit)

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

### 더욱 간단한 풀이 방법 (시간: `O(n)`, 공간: `O(1)`)
- _*링크:* https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/39049/Easy-O(n)-Python-solution

```python
class Solution(object):
    def maxProfit(self, prices):

        profit, min_buy = 0, float('inf')

        for price in prices:
            # 1. 현재 가격과 최소 가격을 비교하여 더 적은 것을 최소 가격으로 업데이트 
            min_buy = min(min_buy, price)

            # 2. 현재 가격에서 최소 가격을 뺀것과 현재 이익을 비교하여 더 높은 것을 현재 이익으로 업데이트
            profit = max(profit, price - min_buy)

        return profit
```

## 회고
_이번 문제는 쉽게 해결했다. 그리고 역시 더욱 간결한 풀이 방법이 있었다!_

_내가 푼 방법과 유사하게 풀었지만, 굳이 조건문을 넣지 않아서 더 간결한 코드였다._