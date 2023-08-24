---
title: LeetCode) Jump Game 알고리즘 문제
slug: "/LeetCode)-Jump-Game-알고리즘-문제"
date: 2023-08-25
tags:
  - Algorithm
  - CodingTest
---

## 55. Jump Game (점프 게임)

- _링크: [https://leetcode.com/problems/jump-game](https://leetcode.com/problems/jump-game)_

> ### 문제 설명
> 
> 정수 배열의 개수가 주어집니다. 사용자는 처음에 배열의 첫 번째 인덱스에 위치하며, 배열의 각 요소는 해당 위치에서 최대 점프 길이를 나타냅니다.
>
> 마지막 인덱스에 도달할 수 있으면 참을 반환하고, 그렇지 않으면 거짓을 반환합니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `nums = [2,3,1,1,4]`
>
> - **Output:**
>   - `true`
>  
> - **Explanation:**
>   - 인덱스 0에서 1로 1단계 이동한 다음 마지막 인덱스까지 3단계 이동합니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `nums = [3,2,1,0,4]`
> 
> - **Output:**
>   - `false`
>  
> - **Explanation:**
>   - 무슨 일이 있어도 항상 인덱스 3에 도달합니다. 최대 점프 길이는 0이므로 마지막 인덱스에 도달할 수 없습니다.
> 
> ### **Constraints:**
>
> - `1 <= nums.length <= 10^4`
> - `0 <= nums[i] <= 10^5`
>
<br></br>

## 풀이 과정

1. 배열 요소가 1개 인지 체크한다. 배열 요소가 1개면 이미 배열의 끝에 도달했기 때문에 `return true` 처리 후 로직을 종료한다.
    ```python
    if len(nums) == 1:
        return True
    ```
    
2. 현재 위치에서 최대 이동 가능한 범위를 나타내는 변수를 초기화한다.
    ```python
    move = nums[0]
    ```

3. 현재 이동 가능한 범위가 배열의 크기보다 큰지 체크한다. 해당 조건에 맞으면 바로 배열의 끝으로 이동 가능하므로 `return true` 처리 후 로직을 종료한다.
    ```python
    if move >= len(nums) - 1:
        return True
    ```

4. 현재 이동 가능한 범위가 배열의 크기보다 작으면 `while` 문을 시작한다.
    ```python
    while move <= len(nums):
    ```

5. 현재 위치에서 더 이동할 수 있는지 여부를 체크한다. 더 이동할 수 있다면 `move` 변수를 다시 이동 가능한 범위만큼 이동시킨다.
    ```python
    if nums[move] == 0:
        이동할 수 없는 경우 이전 위치로 돌아가면서 확인
    else:
        move += nums[move]
    ```

6. 현재 위치에서 더 이동할 수 없다면 이전 위치로 돌아가면서 확인하는 로직을 작성한다. `move` 변수를 `-1` 만큼 이동시키며 순회하는 `for-in` 문을 선언하고, 이전 위치에서 현재 위치로 도달 가능한지 여부를 체크하는 조건문을 작성한다. 조건이 참이면 `move` 변수를 진행 가능한 위치로 업데이트한다. `for-in` 문이 종료되어 더 이상 진행 불가능한 상황이 되면 `return false` 로 로직을 종료한다.
    ```python
    for i in range(move - 1, -1, -1):	    
        # 이전 위치에서 현재 위치로 도달 가능한지 확인
        if i + nums[i] > move:
            # 진행 가능한 위치로 업데이트
            move = i + nums[i]
            break
    
    else:
        return False
    ```

7. `while` 문이 종료될 때 까지 배열의 마지막에 도달하지 못한 경우엔 `return false` 처리 후 로직을 종료한다.
    ```python
    return False
    ```
<br></br>

## 최초 제출 코드
```python
class Solution(object):
    def canJump(self, nums):
                    
        # 1. 배열 요소가 1개면 return true
        if len(nums) == 1:
            return True

        # 2. 현재 위치에서 최대 이동 가능한 범위를 나타내는 변수 초기화
        move = nums[0]
        
        # 3. 이동 가능한 범위가 배열 요소보다 크면 return true
        if move >= len(nums) - 1:
            return True

        while move < len(nums):
            
            # 4. 현재 위치가 배열의 끝에 도달 가능하면 return true
            if move >= len(nums) - 1:
                return True

            # 5-1. 현재 위치에서 더 이동할 수 없는 상황일 때
            if nums[move] == 0:
                
                # 5-1-1. 이전 위치로 돌아가면서 확인
                for i in range(move - 1, -1, -1):
                    
                    # 5-1-1-1. 이전 위치에서 현재 위치로 도달 가능한지 확인
                    if i + nums[i] > move:
                        # 5-1-1-2. 진행 가능한 위치로 업데이트
                        move = i + nums[i]
                        break

                # 5-1-2. 더 이상 진행 불가능한 상황이면 return false
                else:5
                    return False
            
            # 5-2. 현재 위치에서 이동할 수 있다면 다시 이동 가능한 범위만큼 이동시킴
            else:
                move += nums[move]
                
        # 6. 배열의 마지막까지 도달하지 못한 경우 return false
        return False
```
<br></br>

## 1차 수정

1. `[1,2,3]` 혹은 `[1,3,2]` 같은 테스트 케이스에서 배열의 중간 요소가 배열의 크기보다 커질 때, `while` 문 바깥으로 탈출하여 `return false` 로 처리되었다. 그래서 이동 가능한 범위가 배열의 크기보다 큰지 체크하는 조건문을 `while` 문 아래로 옮겨서 해당 케이스를 통과할 수 있도록 처리하였다.
    ```python
    if move >= len(nums) - 1:
        return True
    ```
<br></br>

## 최종 제출 코드
```python
class Solution(object):
    def canJump(self, nums):
                    
        # 1. 배열 요소가 1개면 return true
        if len(nums) == 1:
            return True

        # 2. 현재 위치에서 최대 이동 가능한 범위를 나타내는 변수 초기화
        move = nums[0]

        while move < len(nums):
            # 3. 현재 위치가 배열의 끝에 도달 가능하면 return true
            if move >= len(nums) - 1:
                return True

            # 4-1. 현재 위치에서 더 이동할 수 없는 상황일 때
            if nums[move] == 0:

                # 4-1-1. 이전 위치로 돌아가면서 확인
                for i in range(move - 1, -1, -1):

                    # 4-1-1-1. 이전 위치에서 현재 위치로 도달 가능한지 확인
                    if i + nums[i] > move:
                        # 4-1-1-2. 진행 가능한 위치로 업데이트
                        move = i + nums[i]
                        break

                # 4-1-2. 더 이상 진행 불가능한 상황이면 return false
                else:
                    return False

            # 4-2. 현재 위치에서 이동할 수 있다면 다시 이동 가능한 범위만큼 이동시킴
            else:
                move += nums[move]

        # 5. 이동 가능한 범위가 배열 요소보다 크면 return true
        if move >= len(nums) - 1:
            return True

        # 6. 배열의 마지막까지 도달하지 못한 경우 return false
        return False
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n) + O(n)` = `O(n)`
- `while` 문이 `len(nums)` 만큼 순회하므로 `O(n)` 의 시간 복잡도를 가진다.
- `for-in` 문은 현재 위치에서 이전 위치까지의 거리만큼만 반복하면 되므로 `O(n)` 의 시간 복잡도를 가진다.

### 공간 복잡도: `O(1)`
- 주어진 배열 `nums` 에서 계산 및 수정 작업을 수행하므로 `O(1)` 의 공간 복잡도를 가진다.
<br></br>


## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")

<br></br>

## 다른 풀이 방법

### 매우 간단한 풀이법 (시간: `O(n)`, 공간: `O(1)`)
- _*링크:* https://leetcode.com/problems/jump-game/discuss/2336291/Very-Easy-100(Fully-Explained)(JavaC%2B%2B-Python-JS-C-Python3)

```python
class Solution(object):
    def canJump(self, nums):
        # 1. 현재까지 가능한 최대 점프 거리를 나타내는 변수 curr을 초기화한다.
        curr = nums[0]
        
        # 2. 배열의 두 번째 요소부터 끝까지 반복하는 for-in 문을 선언한다.
        for i in range(1, len(nums)):
            # 3. curr 값이 0 인 경우, 현재 위치에 도달할 수 있는 방법이 없는 것이므로 return false
            if curr == 0:
                return False
            
            # 4. 현재 최대 점프 거리를 -1 함
            curr -= 1
            
            # 5. 현재 최대 점프 거리, nums[i] 중 더 큰 값을 최대 점프 거리로 업데이트
            curr = max(curr, nums[i])

        return True
```

## 회고
_이번 문제는 생각보다 많이 어려워서 푸는데 오래 걸렸다._

_로직을 생각하는 데는 오래 걸리지 않았으나, 코드로 옮기는데에서 시간을 많이 잡아먹었다._

_다 풀고나서 다른 풀이 방법을 보는데 몇줄의 코드로 이 문제를 푸는 방법이 있어서 충격을 먹었다..._

_정말 알고리즘은 같은 문제라도 푸는 사람에 따라서 효율적이냐, 비효율적이냐가 나뉘어지는 것 같다._