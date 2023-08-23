---
title: LeetCode) Remove Element 알고리즘 문제
slug: "/LeetCode)-Remove-Element-알고리즘-문제"
date: 2023-08-23
tags:
  - Algorithm
  - CodingTest
---

## 27. Remove Element (요소 제거)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0027-remove-element](https://github.com/hcgo97/leetcode/tree/master/0027-remove-element)_
- _링크: [https://leetcode.com/problems/remove-element](https://leetcode.com/problems/remove-element)_

> ### 문제 설명
> 
> 정수 배열 `nums`와 정수 `val`이 주어졌을 때, `nums`에서 `val`이 포함된 모든 항목을 제자리에서 제거합니다. 요소의 순서는 변경될 수 있습니다. 그런 다음 `nums`에서 `val`과 같지 않은 요소의 수를 반환합니다.
> 
> `nums`에서 `val`과 같지 않은 요소의 수가 `k`라고 가정하면 다음과 같은 작업을 수행해야 허용됩니다:
> - `nums`의 처음 `k` 요소에 `val`과 같지 않은 요소가 포함되도록 배열 `nums`를 변경합니다. `nums`의 나머지 요소는 `nums`의 크기만큼 중요하지 않습니다.
> - `k`를 반환합니다.
> 
> ### **Custom Judge:**
> 
> - 감독은 다음 코드를 사용하여 솔루션을 테스트합니다:
>     ```
>     int[] nums = [...]; // 입력 배열
>     int val = ...; // 제거할 값
>     int[] expectedNums = [...]; // 올바른 길이의 예상 답안.
>                                 // val과 같은 값이 없는 것으로 정렬됩니다.
>     
>     int k = removeElement(nums, val); // 구현을 호출합니다.
>     
>     assert k == expectedNums.length;
>     sort(nums, 0, k); // nums의 처음 k 요소를 정렬합니다.
>     for (int i = 0; i < actualLength; i++) {
>         assert nums[i] == expectedNums[i];
>     }
>     ```
> - 모든 어설션이 통과하면 솔루션이 승인됩니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `nums = [3,2,2,3]`, `val = 3`
>
> - **Output:**
>   - `2`, `nums = [2,2,_,_]`
>
> - **Explanation:**
>   - 함수는 `nums`의 처음 두 요소가 `2`인 `k = 2`를 반환해야 합니다.
>   - 반환된 `k` 너머에 무엇을 남기든 상관없습니다(따라서 밑줄이 됩니다).
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `nums = [0,1,2,2,3,0,4,2]`, `val = 2`
> 
> - **Output:**
>   - `5`, `nums = [0,1,4,0,3,_,_,_]`
> 
> - **Explanation:**
>   - 함수는 `nums`의 처음 다섯 요소가 `0, 0, 1, 3, 4`를 포함하는 `k = 5`를 반환해야 합니다.
>   - 다섯 요소는 어떤 순서로든 반환될 수 있습니다.
>   - 반환된 `k` 너머에 무엇이 남는지는 중요하지 않습니다(따라서 밑줄이 됩니다).
> 
> ### **Constraints:**
> 
> - `0 <= nums.length <= 100`
> - `0 <= nums[i] <= 50`
> - `0 <= val <= 100`
>
<br></br>

## 풀이 과정

1. `nums` 배열에서 `val` 요소를 모두 삭제한다.
    ```python
    while val in nums:
    	nums.remove(val)
    ```
    
2. `nums` 배열의 길이를 리턴한다.
    ```python
    return len(nums)
    ```

### 최종 제출 코드
```python
class Solution(object):
    def removeElement(self, nums, val):
	# 1. nums 배열에서 val 요소 다 삭제하기
        while val in nums:
	    nums.remove(val)

	# 2. nums 배열의 길이를 리턴
        return len(nums)
```
<br></br>

## 시간 복잡도

### `O(n) * O(n)` = **`O(n^2)`**
- `nums` 배열 내부에 `val` 요소가 없는 경우
  - `O(n)`
- `nums2` 배열 내부에 `val` 요소가 있는 경우
  - `O(n^2)`
<br></br>

## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")
<br></br>

## 다른 풀이 방법

### `O(n)` 시간 복잡도를 갖는 풀이 방법
- _링크: https://leetcode.com/problems/remove-element/discuss/3670940/Best-100-oror-C%2B%2B-oror-JAVA-oror-PYTHON-oror-Beginner-Friendly_
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        index = 0

        for i in range(len(nums)):
            if nums[i] != val:
                nums[index] = nums[i]
                index += 1

        return index
```
1. 삭제대상이 아닌 요소를 이동시킬 위치를 가리키는 `index` 변수를 `0`으로 초기화한다.
2. `nums` 의 각 소요를 반복하는 for 문을 선언한다.
3. 만약 현재 `nums` 요소가 삭제되어야 할 요소 `val` 이 아니라면 현재 `nums` 요소를 `index` 위치로 대체한다.
4. 현재 `index` 위치에 요소가 저장되었으므로 `index` 의 위치를 `index + 1` 만큼 옮긴다.
5. 삭제되지 않은 요소의 갯수인 `index` 변수를 리턴한다.
<br></br>

## 회고

_이번 문제는 난이도가 쉬워서 그런지 어렵지 않게 풀었지만, 시간 복잡도는 `O(n^2)` 로 성능이 좋지 않았다._

_다른 사람들의 풀이를 찾아보니 대부분 `index` 변수를 따로 지정한 뒤, 대상이 아닌 요소를 만나면 `index` 위치로 스왑하는 방법으로 `O(n)` 복잡도의 로직을 구현하고 있었다._

_단지 코드 몇줄 차이로 내가 구현한 로직보다 제곱배나 빠른 로직을 구현한 것이다._

_나는 지금껏 실무를 하면서 자료구조, 알고리즘은 아주 복잡한 기능이 아니라면 굳이 필요할까? 라는 생각을 해 왔었다. 하지만 문제를 풀면 풀 수록 자료구조와 알고리즘을 왜 필수로 익혀야 하는지, 실무에서 얼마나 중요한 건지를 깨닫고 있다. 진작에 깨달았다면 실무에서 기능 구현할 때 성능 최적화에 아주 도움이 됬었을 것이다. 지금이라도 깨우쳐서 다행인걸까?_

_이번 문제 풀이는 잘 기억해뒀다가 다음에 비슷한 문제를 만나게 되면 꼭 적용해봐야겠다. 시간 복잡도를 고려해서 로직을 작성하는 습관을 들여야겠다._