---
title: LeetCode) Minimum Size Subarray Sum 알고리즘 문제
slug: "/LeetCode)-Minimum-Size-Subarray-Sum-알고리즘-문제"
date: 2023-08-28
tags:
  - Algorithm
  - CodingTest
---

## 209. Minimum Size Subarray Sum (최소 크기 부분 배열 합계)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0209-minimum-size-subarray-sum](https://github.com/hcgo97/leetcode/tree/master/0209-minimum-size-subarray-sum)_
- _링크: [https://leetcode.com/problems/minimum-size-subarray-sum](https://leetcode.com/problems/minimum-size-subarray-sum)_

> ### 문제 설명
>
> 양의 정수의 배열과 양의 정수 타깃이 주어졌을 때, 합이 타깃보다 크거나 같은 서브 배열의 최소 길이를 반환합니다. 그러한 하위 배열이 없으면 대신 0을 반환합니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `target = 7`, `nums = [2, 3, 1, 2, 4, 3]`
>
> - **Output:**
>   - `2`
>  
> - **Explanation:**
>   - 하위 배열 `[4, 3]`은 문제 제약 조건에서 최소 길이를 가집니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `target = 4`, `nums = [1, 4, 4]`
> 
> - **Output:**
>   - `1`
>  
> ### **Example 3:**
> 
> - **Input:**
>   - `target = 11`, `nums = [1, 1, 1, 1, 1, 1, 1, 1]`
> 
> - **Output:**
>   - `0`
> 
> ### **Constraints:**
>
> - `1 <= target <= 10^9`
> - `1 <= nums.length <= 10^5`
> - `1 <= nums[i] <= 10^4`
>
<br></br>

## 풀이 과정

1. 시작 지점을 가리키는 포인터 `left`를 초기화한다.
    ```python
    left = 0
    ```
    
2. 배열의 최소 길이를 무한대로 설정한다.
    ```python
    minLength = float('inf')
    ```

3. 현재 부분 배열의 합을 나타내는 변수를 초기화한다.
    ```python
    currentSum = 0
    ```

4. `nums` 배열의 요소만큼 반복하는 `for` 문을 선언한다. 반복마다 `right` 포인터 변수를 `+ 1`만큼 이동한다.
    ```python
    for right in range(len(nums)):
    ```

5. 현재 합계에 `right` 포인터가 가리키고 있는 원소 값을 추가한다.
    ```python
        currentSum += nums[right]
    ```

6. 현재 합계가 목표값 이상인 동안 반복하는 `while` 문을 선언한다.
    ```python
        while currentSum >= target:
    ```

7. 최소 길이를 현재 최소 길이와 현재 부분 배열의 길이 중 작은 값으로 업데이트한다.
    ```python
            minLength = min(minLength, right - left + 1)
    ```

8. 부분 배열의 합에서 `left` 포인터가 가리키는 원소를 빼서 윈도우를 이동시킨다.
    ```python
            currentSum -= nums[left]
    ```

9. `left` 포인터 변수를 `+ 1` 만큼 이동시킨다.
    ```python
            left += 1
    ```

10. `for` 문 이 종료되면 배열의 최소길이를 `return` 한다. 만약 배열의 최소 길이가 할당되지 않았다면 `0`을 `return` 한다.
    ```python
    return minLength if minLength != float('inf') else 0
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def minSubArrayLen(self, target, nums):
        
        # 1. 시작 지점을 가리키는 포인터 left를 초기화한다.
        left = 0
        
        # 2. 배열의 최소 길이를 무한대로 설정한다.
        minLength = float('inf')
        
        # 3. 현재 부분 배열의 합을 나타내는 변수를 초기화한다.
        currentSum = 0

        # 4. nums 배열의 요소만큼 반복하는 for 문을 선언한다.
        # 반복마다 right 포인터 변수를 + 1만큼 이동한다.
        for right in range(len(nums)):
            # 5. 현재 합계에 right 포인터가 가리키고 있는 원소 값을 추가한다.
            currentSum += nums[right]

            # 6. 현재 합계가 목표값 이상인 동안 반복하는 while 문을 선언한다.
            while currentSum >= target:
                # 7. 최소 길이를 현재 최소 길이와 현재 부분 배열의 길이 중 작은 값으로 업데이트한다.
                minLength = min(minLength, right - left + 1)
                
                # 8. 부분 배열의 합에서 left 포인터가 가리키는 원소를 빼서 윈도우를 이동시킨다.
                currentSum -= nums[left]
                
                # 9. left 포인터 변수를 + 1 만큼 이동시킨다.
                left += 1

        # 10. for 문 이 종료되면 배열의 최소길이를 return 한다.
        # 만약 배열의 최소 길이가 할당되지 않았다면 0을 return 한다.
        return minLength if minLength != float('inf') else 0
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n)`
- 배열을 한 번 순회하면서 각 원소를 한 번씩 처리하므로 `O(n)` 의 시간 복잡도를 가진다.

### 공간 복잡도: `O(1)`
-  입력 배열 외에 추가적인 배열 공간을 사용하지 않으므로 `O(1)` 의 공간 복잡도를 가진다.
<br></br>

## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")
<br></br>

## 회고
_이번 문제는 도저히 감이 잡히지 않아서 해답을 참고하였는데, 투 포인터와 슬라이딩 윈도우 방법을 섞어서 푸는 문제였다._

_`left` 와 `right` 두 개의 포인터가 배열을 순회하면서 부분 배열의 합을 조절하고, 길이를 최소화하여 최종적으로 부분 배열의 최소 길이를 반환하는 방식이다._

_투 포인터 방법은 숙지하였지만, 슬라이딩 윈도우 방법은 이론적으로만 숙지하고 있었던 부분이라 실제 문제에 적용시키지 못해 아쉬웠다._

_이번에 확실히 숙지하였으니 다음엔 적용해보도록 해야겠다._
