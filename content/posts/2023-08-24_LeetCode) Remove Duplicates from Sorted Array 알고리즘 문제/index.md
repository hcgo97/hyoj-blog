---
title: LeetCode) Remove Duplicates from Sorted Array 알고리즘 문제
slug: "/LeetCode)-Remove-Duplicates-from-Sorted-Array-알고리즘-문제"
date: 2023-08-24
tags:
  - Algorithm
  - CodingTest
---

## 26. Remove Duplicates from Sorted Array (정렬된 배열에서 중복 제거)

- _링크: [https://leetcode.com/problems/remove-duplicates-from-sorted-array](https://leetcode.com/problems/remove-duplicates-from-sorted-array)_

> ### 문제 설명
> 
> 정수 배열의 숫자가 감소하지 않는 순서로 정렬되어 있을 때, 각 고유 요소가 한 번만 나타나도록 중복된 요소를 제자리에서 제거합니다. 요소의 상대적 순서는 동일하게 유지해야 합니다. 그런 다음 고유 요소의 개수를 숫자로 반환합니다.
>
> `nums`의 고유 요소 수를 `k`라고 가정하고, 이를 허용하려면 다음과 같은 작업을 수행해야 합니다:
> - `nums`의 처음 `k` 요소에 `val`과 같지 않은 요소가 포함되도록 배열 `nums`를 변경합니다. `nums`의 나머지 요소는 `nums`의 크기만큼 중요하지 않습니다.
> - `k`를 반환합니다.
> 
> ### **Custom Judge:**
> 
> - 감독은 다음 코드를 사용하여 솔루션을 테스트합니다:
>     ```
>     int[] nums = [...]; // 입력 배열
>     int[] expectedNums = [...]; // 올바른 길이의 예상 답안
>
>     int k = removeDuplicates(nums); // 구현을 호출합니다.
>
>     assert k == expectedNums.length;
>     for (int i = 0; i < k; i++) {
>         assert nums[i] == expectedNums[i];
>     }
>     ```
> - 모든 어설션이 통과하면 솔루션이 승인됩니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `nums = [1,1,2]`
>
> - **Output:**
>   - `2`, `nums = [1,2,_]`
>
> - **Explanation:**
>   - 함수는 `k = 2`를 반환해야 하며, `nums`의 처음 두 요소는 각각 `1`과 `2`입니다.
>   - 반환된 `k` 너머에 무엇을 남기든 상관없습니다(따라서 밑줄이 됩니다).
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `nums = [0,0,1,1,1,2,2,3,3,4]`
> 
> - **Output:**
>   - `5`, `nums = [0,1,2,3,4,_,_,_,_,_]`
> 
> - **Explanation:**
>   - 함수는 `k = 5`를 반환해야 하며, `nums`의 처음 다섯 요소는 각각 `0, 1, 2, 3, 4`입니다.
>   - 반환된 `k` 너머에 무엇이 남는지는 중요하지 않습니다(따라서 밑줄이 됩니다).
> 
> ### **Constraints:**
>
> - `1 <= nums.length <= 3 * 10^4`
> - `100 <= nums[i] <= 100`
> - `nums`는 감소하지 않는 순서(ASC) 로 정렬됩니다.
>
<br></br>

## 풀이 과정

1. 중복이 아닌 요소들을 담을 `set` 을 생성한다.
  - `nums` 배열에서 해당 요소의 중복 여부를 `set` 에 해당 요소가 있는지의 여부로 판단할 것이다.
    ```python
    numSet = set()
    ```
    
2. 중복이 아닌 요소의 위치를 지정할 변수를 초기화한다.   
    ```python
    index = 0
    ```

3. `nums` 의 현재 요소가 중복된 원소인지 여부를 검사하는 조건문을 추가한다.   
    ```python
    for num in nums:
        if num not in numSet:
    ```

4. 해당 조건에 해당하면 현재 요소는 중복이 아니므로 `index` 위치로 옮긴 후, `set` 에 추가하여 중복이라는 표시를 한다.   
    ```python
        nums[index] = num
        index += 1
        numSet.add(num)
    ```

5. `for - in` 문이 종료되면 `nums` 의 모든 요소를 중복 검사 한 것 이므로 중복이 아닌 요소의 개수인 `index` 를 리턴한다.
    ```python
    return index
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def removeDuplicates(self, nums):
        
        # 중복이 아닌 요소들을 담을 set 생성
        numSet = set()
        
        # 중복이 아닌 요소들의 위치를 지정할 변수 초기화
        index = 0

        for num in nums:
            
            # 1. 현재 요소가 set 에 없는 요소라면
            if num not in numSet:
                
                # 2. index 위치로 현재 요소 옮기기
                nums[index] = num
                
                # 3. index 위치 +1 만큼 옮김
                index += 1

                # 4. set 에 추가
                numSet.add(num)

	# 5. 중복되지 않은 요소의 갯수 리턴
        return index
```
<br></br>

## 시간 복잡도

### `O(n)`
- `nums` 요소의 개수만큼 중복 검사를 반복하므로 `O(n)` 의 시간복잡도를 가진다.
<br></br>


## 문제 풀이 기록
![hyoj leet code submit history](img1.png "hyoj leet code submit history")

<br></br>

## 다른 풀이 방법

### 두 포인터를 사용하는 방법 (`O(n)`)
- _*링크:* https://leetcode.com/problems/remove-duplicates-from-sorted-array/discuss/2801641/Daily-LeetCoding-Challenge-November-Day-11_

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        # 1. 중복 제거된 요소의 개수와 새로운 배열의 인덱스를 초기화
        count, j = 1, 1

        # 2. 배열을 순회하면서 중복을 제거하는 반복문 시작
        for i in range(1, len(nums)):

	    # 3. 현재 요소와 이전 요소가 같으면 중복이므로 무시하고 다음 요소로 넘어감
            if nums[i] == nums[i-1]:
                continue

	    # 4. 중복이 아닌 경우, count를 증가시키고 중복 제거된 요소를 새로운 배열의 j 위치에 저장
            count += 1
            nums[j] = nums[i]
            j += 1

	# 5. 중복 제거된 요소의 개수 반환
        return count
```