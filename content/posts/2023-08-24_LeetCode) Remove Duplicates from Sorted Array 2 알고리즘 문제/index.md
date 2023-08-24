---
title: LeetCode) Remove Duplicates from Sorted Array 2 알고리즘 문제
slug: "/LeetCode)-Remove-Duplicates-from-Sorted-Array-2-알고리즘-문제"
date: 2023-08-24
tags:
  - Algorithm
  - CodingTest
---

## 80. Remove Duplicates from Sorted Array 2 (정렬된 배열에서 중복 제거 2)

- _링크: [https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)_

> ### 문제 설명
>
> 정수 배열의 숫자가 감소하지 않는 순서로 정렬되어 주어졌을 때, 각 고유 요소가 최대 두 번만 나타나도록 중복된 부분을 제자리에서 제거합니다. 요소의 상대적 순서는 동일하게 유지해야 합니다.
>
> 일부 언어에서는 배열의 길이를 변경할 수 없으므로 대신 결과를 배열 번호의 첫 번째 부분에 배치해야 합니다. 좀 더 공식적으로 말하자면, 중복을 제거한 후 요소가 k 개 있는 경우 nums의 처음 k 개 요소가 최종 결과를 보유해야 합니다. 처음 k 요소 너머에 무엇이 남는지는 중요하지 않습니다.
>
> nums의 처음 k 슬롯에 최종 결과를 배치한 후 k를 반환합니다.
>
> 다른 배열을 위해 추가 공간을 할당하지 마십시오. O(1)의 추가 메모리로 입력 배열을 제자리에서 수정하여 이 작업을 수행해야 합니다.
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
>   - `nums = [1,1,1,1,2,2,3]`
> 
> - **Output:**
>   - `5`, `nums = [1,1,2,2,3,_]`
> 
> - **Explanation:**
>   - 함수는 `k = 5`를 반환해야 하며, `nums`의 처음 다섯 요소는 각각 `1, 1, 2, 2, 3`입니다.
>   - 반환된 `k` 너머에 무엇이 남는지는 중요하지 않습니다(따라서 밑줄이 됩니다).
>
> ### **Example 2:**
> 
> - **Input:**
>   - `nums = [0,0,1,1,1,1,2,3,3]`
> 
> - **Output:**
>   - `7`, `nums = [0,0,1,1,2,3,3,_,_]`
> 
> - **Explanation:**
>   - 함수는 `k = 7`을 반환해야 하며, `nums`의 처음 일곱 요소는 각각 `0, 0, 1, 1, 2, 3, 3`입니다.
>   - 반환된 `k` 너머에 무엇이 남는지는 중요하지 않습니다(따라서 밑줄이 됩니다).
> 
> ### **Constraints:**
>
> `1 <= nums.length <= 3 * 10^4`
> `-10^4 <= nums[i] <= 10^4`
> - `nums`는 감소하지 않는 순서(ASC) 로 정렬됩니다.
>
<br></br>

## 풀이 과정

1. nums 배열 요소가 2개 이하면 중복 검사를 할 필요가 없으므로 바로 return 하는 조건문을 추가한다.
   ```python
   if len(nums) <= 2:
   	return len(nums)
   ```

2. 최대 2번 까지 요소들끼리 중복이 가능하므로 중복이 아닌 요소의 위치를 지정할 index 변수를 2로 초기화한다.
    ```python
    index = 2
    ```
    
3. nums 배열을 순회하는 for in 문을 선언한다. 중복 허용이 2번까지 가능하므로 i의 증가량은 2로 지정한다.
    ```python
    for i in range(2, len(nums)):
    ```

4. 중복이 허용되는 범위를 벗어나면, 중복이 허용되는 범위 내에 있는 nums 요소를 index 위치에 저장하는 로직을 추가한다.
    ```python
        if nums[i] != nums[index - 2]:
            nums[index] = nums[i]
            index += 1
    ```

5. nums 배열 순회 완료 후, 중복이 제거된 nums 요소의 개수를 return 한다.
    ```python
    return index
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def removeDuplicates(self, nums):
        
        # 1. nums 배열 요소가 2개 이하면 바로 return
        if len(nums) <= 2:
            return len(nums)
        
        # 2. 최대 두 번까지 중복이 가능하므로 2로 초기화
        index = 2
        
        for i in range(2, len(nums)):
            
            # 3. 중복이 허용되는 범위를 벗어나면 
            if nums[i] != nums[index - 2]:
                
                # 4. 중복이 허용되는 범위 내에 있는 nums 요소를 index 위치에 저장
                nums[index] = nums[i]
                
                # 5. 다음 중복 허용 범위로 index 위치를 옮김
                index += 1
        
        # 6. 중복 제거된 nums 요소 개수 return
        return index
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n)`
- `nums` 요소의 개수만큼 중복 검사를 반복하므로 `O(n)` 의 시간복잡도를 가진다.
### 공간 복잡도: `O(1)`
- 추가적인 배열을 사용하지 않고 입력받은 배열 nums 내에서 작업을 수행하므로 `O(1)` 의 공간복잡도를 가진다.
<br></br>


## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")
<br></br>

## 다른 풀이 방법

### 3 ~ 5 줄의 간단한 코드 (`O(n)`)
- _*링크:* https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/discuss/27976/3-6-easy-lines-C%2B%2B-Java-Python-Ruby

```python
class Solution(object):
    def removeDuplicates(self, nums):
	# 중복을 최대 2 번까지만 허용할 인덱스를 초기화
        i = 0
    
        for n in nums:
            # i < 2: 처음 두 개의 요소는 중복이 허용되므로 바로 저장하고 인덱스 증가
            # n > nums[i-2]: 중복이 허용되는 범위를 검사: 현재 요소가 두 칸 앞의 요소보다 큰 경우만 허용
            if i < 2 or n > nums[i-2]:
                nums[i] = n
                i += 1

	# 중복 제거 후의 요소 개수를 반환
        return i
```