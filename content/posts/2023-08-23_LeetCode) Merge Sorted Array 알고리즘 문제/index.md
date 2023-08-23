---
title: LeetCode) Merge Sorted Array 알고리즘 문제
slug: "/LeetCode)-Merge-Sorted-Array-알고리즘-문제"
date: 2023-08-23
tags:
  - Algorithm
  - CodingTest
---

## 88. Merge Sorted Array (정렬된 배열 병합)
- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0088-merge-sorted-array](https://github.com/hcgo97/leetcode/tree/master/0088-merge-sorted-array)_
- _문제 링크: [https://leetcode.com/problems/merge-sorted-array](https://leetcode.com/problems/merge-sorted-array/)_

> ### 문제 설명
> 
> 감소하지 않는 순서로 정렬된 두 개의 정수 배열 `nums1`과 `nums2`가 주어지고, `nums1`과 `nums2`의 요소 수를 각각 나타내는 두 개의 정수 `m`과 `n`이 주어집니다.
> 
> `nums1`과 `nums2`를 감소하지 않는 순서로 정렬된 단일 배열로 병합합니다.
> 
> 최종 정렬된 배열은 함수에 의해 반환되지 않고 `nums1` 배열 안에 저장되어야 합니다. 이를 위해 `nums1`의 길이는 `m + n`이며, 첫 번째 `m` 요소는 병합해야 하는 요소를 나타내고 마지막 `n` 요소는 `0`으로 설정되어 무시해야 합니다. `nums2`의 길이는 `n`입니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `nums1 = [1,2,3,0,0,0]`, `m = 3`, `nums2 = [2,5,6]`, `n = 3`
> 
> - **Output:**
>   - `[1,2,2,3,5,6]`
> 
> - **Explanation:**
>   - 병합하는 배열은 `[1,2,3]` 및 `[2,5,6]`입니다. 
>   - 병합 결과는 `[1,2,2,3,5,6]`이며 밑줄이 그어진 요소는 `nums1`에서 가져온 것입니다.
>
> ### **Example 2:**
> 
> - **Input:**
>   - `nums1 = [1]`, `m = 1`, `nums2 = []`, `n = 0`
> 
> - **Output:**
>   - `[1]`
> 
> - **Explanation:**
>   - 병합하는 배열은 `[1]`과 `[]`입니다.
>   - 병합 결과는 `[1]`입니다.
> 
> ### **Example 3:**
> 
> - **Input:**
>   - `nums1 = [0]`, `m = 0`, `nums2 = [1]`, `n = 1`
>
> - **Output:**
>   - `[1]`
> 
> - **Explanation:**
>   - 병합하는 배열은 `[]` 및 `[1]`입니다.
>   - 병합의 결과는 `[1]`입니다.
>   - `m = 0`이므로 `nums1`에는 요소가 없습니다. `0`은 병합 결과가 `nums1`에 맞을 수 있도록 하기 위해서만 존재합니다.
> 
> ### **Constraints:**
> 
> - `nums1.length == m + n`
> - `nums2.length == n`
> - `0 <= m, n <= 200`
> - `1 <= m + n <= 200`
> - `-10^9 <= nums1[i], nums2[j] <= 10^9`
>
<br></br>

## 풀이 과정

1. 먼저 `nums1` 배열에 `nums2` 배열을 합친다.
    ```python
    nums1 += nums2
    ```

2. 합쳐진 `nums1` 배열 정렬을 정렬한다.
    ```python
    nums1.sort()
    ```

3. `nums1` 배열에서 0인 요소만 삭제한다.
   - 처음엔 for-in 문을 사용하여 0인 요소를 삭제하려 했으나 삭제되지 않았다.
       ```python
       nums1 = [x for x in nums1 if x != 0]
       ```
   - 이유는 함수 내부에서는 `nums1` 이 수정되었지만, 함수가 끝나면 `nums1` 의 수정 내역이 삭제되기 때문이다.
   - 수정된 함수 내역을 반영하려면 `return nums1` 을 하여 반영해야하는데, 해당 문제는 return 타입이 따로 지정되어 있지 않기 때문에 `nums1` 의 수정 내역을 반영 할 수 없었다.
   - 따라서 아래와 같이 while 문으로 처리하였다.
       ```python
       while 0 in nums1:
           nums1.remove(0)
       ```

### 최초 제출 코드
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        # 1. nums1 요소와 nums2 요소를 합침
        nums1 += nums2
        
        # 2. 정렬
        nums1.sort()
            
        # 3. 0인 요소만 삭제
        while 0 in nums1:
	    nums1.remove(0)
```
<br></br>

## 1차 수정 - 조건문 추가

1. `nums2` 요소가 존재하는 경우에만 `nums1` 요소와 합치면 되므로 조건문을 추가하였다.
    ```python
    if n != 0:
        nums1 += nums2
    ```

2. `sort()` 함수를 사용해야 하는 경우는 `nums1` + `nums2` 한 결과 일때 밖에 없으므로 해당 조건문을 추가하였다.
    - `nums2` 요소만 존재하는 경우일때는 이미 정렬되어 있는 `nums2` 배열을 `nums1` 에 추가한 경우이므로 `sort()` 함수를 사용하지 않아도 된다.
    ```python
    if m != 0 and n != 0:
        nums1.sort()
    ```

### 1차 수정 코드
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        # 1. nums2 요소가 있는 경우에만 nums1 요소와 nums2 요소를 합침
        if n != 0:
            nums1 += nums2

	    # 2. nums1 요소와 nums2 요소가 둘다 있는데 합친 경우라면 정렬
	    if m != 0:
	        nums1.sort()
            
        # 3. nums1 에서 0인 요소만 삭제
        while 0 in nums1:
            nums1.remove(0)
```
<br></br>

## 2차 수정 - 문제를 잘못 이해한 부분 수정

- 0의 값을 가지는 요소는 모두 삭제해야 하는 것으로 문제를 잘못 이해하고 있었다.
- 0인 요소는 무조건 삭제하는 것이 아니라, `nums1` 마지막 요소부터 `nums2` 요소 개수 만큼의 0인 요소를 삭제 해야하기 때문에 해당하는 조건문을 추가하고 잘못된 코드를 삭제하였다.
    ```python
    if n > 0:
        del nums1[-n:]
    ```

### 최종 제출 코드
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        # 1. nums2 요소가 있는 경우에만
        if n > 0:
            # 2. nums1 마지막 요소부터 num2 요소 개수만큼 삭제
            del nums1[-n:]
            
            # 3. nums1 요소와 nums2 요소를 합침
            nums1 += nums2
            
            # 4. nums1 요소와 nums2 요소가 둘다 있는데 합친 경우라면 정렬
            if m > 0:
                nums1.sort()
```
<br></br>

## 시간 복잡도
### `O(1) + O(n) + O(n) + O(n log n)` = **`O(n log n)`**
- `nums1` 요소만 있는 경우
    - `O(1)`
- `nums2` 요소만 있는 경우
    - `O(n)`
- `nums1` 요소와 `nums2` 요소가 둘 다 있는 경우
    - `O(n log n)`
<br></br>

## 문제 풀이 기록
![hyoj leet code submit history](img1.png "hyoj leet code submit history")
<br></br>

## 다른 풀이 방법

### `O(n)` 시간 복잡도를 갖는 풀이 방법
- _링크: [https://leetcode.com/problems/merge-sorted-array/discuss/2360538/Easy-0-ms-100-(Fully-Explained)(Java-C%2B%2B-Python-JS-C-Python3)](https://leetcode.com/problems/merge-sorted-array/discuss/2360538/Easy-0-ms-100-(Fully-Explained)(Java-C%2B%2B-Python-JS-C-Python3))_
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        # Initialize nums1's index
        i = m - 1
        # Initialize nums2's index
        j = n - 1
        # Initialize a variable k to store the last index of the 1st array...
        k = m + n - 1
        while j >= 0:
            if i >= 0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                k -= 1
                i -= 1
            else:
                nums1[k] = nums2[j]
                k -= 1
                j -= 1
```
1. `nums1` 의 마지막 요소(`m - 1`)를 가리키는 포인터 `i` 를 설정한다.
2. `nums2` 의 마지막 요소(`n - 1`)를 가리키는 포인터 `j` 를 설정한다.
3. `nums1`, `nums2` 의 요소들을 합쳤을 때의 마지막 요소(`m + n - 1`)를 가리키는 포인터 `k` 를 설정한다.
4. 포인터 `j`가 0보다 같거나 클 경우
    1. `nums1[i]` 요소와 `nums[j]` 요소를 비교 후, 더 큰 요소를 `nums1[k]` 에 대체한다.
    2. 포인터 `k` 와 대체한 요소의 포인터를 -1 만큼 옮긴다.
    3. 포인터 `j` 가 -1 이 될때까지 반복한다.
5. 포인터 `j` 가 0보다 작을 경우에는 `nums2` 의 요소가 존재하지 않는다는 것이므로 로직이 종료된다.
<br></br>

## 회고
_학부 시절 이후로는 처음으로 알고리즘 문제를 풀어본건데 eazy 난이도임에도 불구하고 생각보다 어렵게 느껴져서 당황스러웠다._

_여러번의 수정 끝에 코드가 통과되었을때는 개발을 처음 시작했었던 때와 같은 짜릿한 희열이 느껴졌다._

_앞으로도 꾸준히 문제를 풀어서 지금보단 더 수월하게 풀 수 있도록 노력해야겠다._

