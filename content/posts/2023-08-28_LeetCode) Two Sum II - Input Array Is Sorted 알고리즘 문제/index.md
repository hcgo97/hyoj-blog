---
title: LeetCode) Two Sum II - Input Array Is Sorted 알고리즘 문제
slug: "/LeetCode)-Two-Sum-II-Input-Array-Is-Sorted-알고리즘-문제"
date: 2023-08-28
tags:
  - Algorithm
  - CodingTest
---

## 167. Two Sum II - Input Array Is Sorted (두 수의 합계 II - Input 은 정렬된 배열)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0167-two-sum-ii-input-array-is-sorted](https://github.com/hcgo97/leetcode/tree/master/0167-two-sum-ii-input-array-is-sorted)_
- _링크: [https://leetcode.com/problems/two-sum-ii-input-array-is-sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)_

> ### 문제 설명
>
> 이미 감소하지 않는 순서로 정렬된 정수의 1 인덱스 배열이 주어졌을 때, 특정 목표 수에 합산되는 두 개의 수를 구합니다. 이 두 숫자를 `numbers[index1]` 및 `numbers[index2]`로 하고, `1 <= index1 < index2 < numbers.length`로 합니다.
>
> 두 숫자의 인덱스인 `index1`과 `index2`의 인덱스에 `1`을 더한 길이 `2`의 정수 배열 `[index1, index2]`를 반환합니다.
>
> 테스트는 정확히 하나의 해가 나오도록 생성됩니다. 동일한 요소를 두 번 사용할 수 없습니다.
>
> 솔루션은 일정한 추가 공간만 사용해야 합니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `numbers = [2, 7, 11, 15]`, `target = 9`
>
> - **Output:**
>   - `[1, 2]`
>  
> - **Explanation:**
>   - `2`와 `7`의 합은 `9`입니다. 따라서 `index1 = 1`, `index2 = 2`입니다. 우리는 `[1, 2]`를 반환합니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `numbers = [2, 3, 4]`, `target = 6`
> 
> - **Output:**
>   - `[1, 3]`
>  
> - **Explanation:**
>   - `2`와 `4`의 합은 `6`입니다. 따라서 `index1 = 1`, `index2 = 3`입니다. 우리는 `[1, 3]`을 반환합니다.
>  
> ### **Example 3:**
> 
> - **Input:**
>   - `numbers = [-1, 0]`, `target = -1`
> 
> - **Output:**
>   - `[1, 2]`
>  
> - **Explanation:**
>   - `-1`과 `0`의 합은 `-1`입니다. 따라서 `index1 = 1`, `index2 = 2`입니다. 우리는 `[1, 2]`를 반환합니다.
> 
> ### **Constraints:**
>
> - `2 <= numbers.length <= 3 * 10^4`
> - `-1000 <= numbers[i] <= 1000`
> - 숫자는 감소하지 않는(`desc`) 순서로 정렬됩니다.
> - `-1000 <= target <= 1000`
> - 테스트는 정확히 하나의 솔루션만 존재하도록 생성됩니다.
>
<br></br>

## 풀이 과정

1. 투 포인터 방법을 사용하기 위해 left, right 변수를 선언한다. left 는 numbers[0] (배열의 가장 첫번째), right 는 numbers[len(index) - 1] (배열의 가장 마지막) 에 위치하도록 초기화한다.
    ```python
    left = 0
    right = len(numbers) - 1
    ```
    
2. 배열의 길이만큼 반복하는 for 문을 선언한다.
    ```python
    for i in range(len(numbers) - 1):
    ```

3. target 과 left, right 을 더한 값을 비교한다.
   - target 과 같으면 left, right 를 +1 씩해서 return 한다.
   - target 보다 크면(<) right 를 -1 해서 포인터 위치를 옮긴다.
   - target 보다 작으면(>) left 를 +1 해서 포인터 위치를 옮긴다.
    ```python
        if target == numbers[left] + numbers[right]:
            return [left + 1, right + 1]
            
        if target < numbers[left] + numbers[right]:
            right -= 1

        if target > numbers[left] + numbers[right]:
            left += 1
    ```
<br></br>

## 최초 제출 코드
```python
class Solution(object):
    def twoSum(self, numbers, target):
        
        # 1. 투 포인터 방법 사용하기 위해 left, right 변수 선언
        # left 는 numbers[0] (배열의 가장 첫번째), right 는 numbers[len(index) - 1] (배열의 가장 마지막) 에 위치하도록 초기화
        left = 0
        right = len(numbers) - 1
        
        # 2. 배열의 길이만큼 반복하는 for 문 선언
        for i in range(len(numbers) - 1):

            # 3. target 과 left, right 을 더한 값을 비교
            if target == numbers[left] + numbers[right]:
                # 3-1. target 과 같으면 left, right 를 +1 씩해서 return
                return [left + 1, right + 1]
            
            if target < numbers[left] + numbers[right]:
                # 3-2. target 보다 크면(<) right 를 -1 해서 포인터 위치를 옮김
                right -= 1

            if target > numbers[left] + numbers[right]:
                # 3-3. target 보다 작으면(>) left 를 +1 해서 포인터 위치를 옮김
                left += 1
```
<br></br>

## 1차 수정

1. `2 <= numbers.length <= 3 * 10^4` 라는 제약 조건이 있으므로, numbers 배열 요소가 2개일 때는 index 1, 2 를 return 하는 조건문을 추가한다.
    ```python
    if len(numbers) == 2:
        return [1, 2]
    ```

2. numbers[left] + numbers[right] 을 더한 변수인 sumNumbers 를 선언하여 코드를 간결하게 하였다.
    ```python
    sumNumbers = numbers[left] + numbers[right]
    ```

2. for 문 내부의 조건문을 간결하게 정리하였다.
    ```python
        if target < sumNumbers:
            right -= 1
    
        elif target > sumNumbers:
            left += 1
    
        else:
            return [left + 1, right + 1]
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def twoSum(self, numbers, target):

        # 1. numbers 배열 요소가 2개밖에 없으면 index 1, 2 를 return
        if len(numbers) == 2:
            return [1, 2]
        
        # 2. 투 포인터 방법 사용하기 위해 left, right 변수 선언
        # left 는 numbers[0] (배열의 가장 첫번째), right 는 numbers[len(index) - 1] (배열의 가장 마지막) 에 위치하도록 초기화
        left = 0
        right = len(numbers) - 1
        
        # 3. 배열의 길이만큼 반복하는 for 문 선언
        for i in range(len(numbers) - 1):
            sumNumbers = numbers[left] + numbers[right]
            
            # 4. target 과 left, right 을 더한값을 비교한다.
            if target < sumNumbers:
                # 4-1. target 보다 크면(<) right 를 -1 해서 포인터 위치를 옮김
                right -= 1

            elif target > sumNumbers:
                # 4-2. target 보다 작으면(>) left 를 +1 해서 포인터 위치를 옮김
                left += 1
                
            else:
                # 4-3. target 과 같으면 left, right 를 +1 씩해서 return
                return [left + 1, right + 1]
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n)`
- for 문은 배열의 요소 수 만큼 반복되므로 `O(n)` 의 시간 복잡도를 가진다.

### 공간 복잡도: `O(1)`
-  입력 배열 외에 추가적인 배열 공간을 사용하지 않으므로 `O(1)` 의 공간 복잡도를 가진다.
<br></br>


## 문제 풀이 기록

![image](https://github.com/hcgo97/leetcode/assets/72455719/d4dfcf96-70ed-4f61-99ef-ccdf4844be23)
<br></br>

## 다른 풀이 방법

### Binary Search(이진 탐색) 을 활용한 방법 (시간: `O(log n)`, 공간: `O(1)`)
- _*링크:* https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/discuss/51249/Python-different-solutions-(two-pointer-dictionary-binary-search)
```python
class Solution:
    def twoSum(self, numbers, target):
        # 1. 배열의 길이만큼 반복하는 for 문 선언
        for i in range(len(numbers)):

	    # 2. 이진 탐색을 위한 포인터 변수 l, r 설정
	    l, r = i+1, len(numbers)-1

	    # 3. 현재 원소에서 목표값을 뺀 값을 저장
	    tmp = target - numbers[i]
	        
	    # 4. 이진 탐색 실행
	    while l <= r:
	        # 5. 중간 인덱스 계산
	        mid = l + (r-l)//2
	            
	        # 5-1. 중간 값이 tmp와 같다면 (두 수의 합을 찾았다면) 해당 두 수의 인덱스를 +1 해서 return
	        if numbers[mid] == tmp:
		    return [i+1, mid+1]

	        # 5-2. 중간 값이 tmp보다 작다면(<), tmp 는 더 큰 값이므로 l 포인터를 오른쪽으로 +1 만큼 옮김
	        elif numbers[mid] < tmp:
		    l = mid+1

	        # 5-3. 중간 값이 tmp보다 크다면(>), tmp는 더 작은 값이므로 r 포인터를 오른쪽으로 -1 만큼 옮김
	        else:
		    r = mid-1
```
<br></br>

## 회고
_이번 문제는 알고리즘을 공부하며 학습한 투 포인터 방법을 사용하여 푼 첫 문제이다._

_투 포인터 방법 외에도 학부시절 자료구조 시간에 배웠던 이진탐색 방법으로도 풀 수 있는 방법이 있었다._

_투 포인터 방법이 O(n), 이진 탐색 방법이 O(log n) 이므로 이번 문제는 이진탐색 방법으로 푸는게 더 효율적인 방법이었다._

_알고리즘을 하나 더 배웠으므로, 이제 다음에 비슷한 문제가 나오면 시간 복잡도를 고려하여 어떤 알고리즘으로 문제를 풀어야할지 생각해서 코드를 작성해야겠다._