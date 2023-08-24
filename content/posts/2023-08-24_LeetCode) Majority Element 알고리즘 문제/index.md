---
title: LeetCode) Majority Element 알고리즘 문제
slug: "/LeetCode)-Majority-Element-알고리즘-문제"
date: 2023-08-24
tags:
  - Algorithm
  - CodingTest
---

## 169. Majority Element (다수 요소)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0169-majority-element](https://github.com/hcgo97/leetcode/tree/master/0169-majority-element)_
- _링크: [https://leetcode.com/problems/majority-element](https://leetcode.com/problems/majority-element)_

> ### 문제 설명
> 
> 크기가 n인 배열의 개수가 주어졌을 때, 다수 요소를 반환합니다.
> 
> 다수 요소는 ⌊n / 2⌋ 이상 나타나는 요소입니다. 다수 요소는 배열에 항상 존재한다고 가정할 수 있습니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `nums = [3,2,3]`
>
> - **Output:**
>   - `3`
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `nums = [2,2,1,1,1,2,2]`
> 
> - **Output:**
>   - `2`
> 
> ### **Constraints:**
>
> - `n == nums.length`
> - `1 <= n <= 5 * 10^4`
> - `-10^9 <= nums[i] <= 10^9`
>
<br></br>

## 풀이 과정

1. 배열 요소가 1개 밖에 없을 경우의 조건문을 추가한다.
    ```python
    if len(nums) == 1:
        return nums[0]
    ```
    
2. sort() 함수로 배열을 정렬한다.
    ```python
    nums.sort()
    ```

3. 배열의 정중앙 index 를 구한다. 배열을 정렬했으므로 정중앙에는 항상 과반수 이상인 요소가 위치하게 된다.
    ```python
    index = len(nums) // 2
    ```

4. 배열의 정중앙 index 에 위치한 요소를 return 한다.
    ```python
    return nums[index]
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def majorityElement(self, nums):
        
        # 1. 배열 요소가 1개 밖에 없으면 바로 return
        if len(nums) == 1:
            return nums[0]
        
        # 2. 배열 정렬
        nums.sort()
        
        # 3. 정중앙에 위치한 index 구함
        index = len(nums) // 2
    
        # 4. 정중앙에 위치한 요소 return
        return nums[index]
```
<br></br>

## 시간 복잡도

### `O(n log n)`
- `sort()` 함수를 사용하여 정렬을 진행하므로 `O(n log n)` 의 시간 복잡도를 가진다.
<br></br>


## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")

<br></br>

## 다른 풀이 방법

### Boyer-Moore Voting 알고리즘을 사용하는 방법 (`O(n)`)
- _*링크:* https://leetcode.com/problems/majority-element/discuss/2379248/Very-Easy-100(Fully-Explained)(C%2B%2B-Java-Python-JS-C-Python3)

```python
class Solution(object):
    def majorityElement(self, nums):

	# 과반 요소를 저장하는 변수 초기화
        sol = None

        # 현재 후보 과반 요소의 등장 횟수 초기화
        cnt = 0
        
        for i in nums:
            if cnt == 0:

		# 현재 후보 과반 요소로 설정
                sol = i

	    # 요소가 현재 후보와 같으면 등장 횟수 증가, 다르면 감소
            cnt += (1 if i == sol else -1)

	# 과반 요소 반환
        return sol
```