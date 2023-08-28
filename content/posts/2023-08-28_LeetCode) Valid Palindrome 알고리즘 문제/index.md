---
title: LeetCode) Valid Palindrome 알고리즘 문제
slug: "/LeetCode)-Valid-Palindrome-알고리즘-문제"
date: 2023-08-28
tags:
  - Algorithm
  - CodingTest
---

## 125. Valid Palindrome (앞 뒤가 똑같은 문자열(팰린드롬)인지 여부)

- _GitHub 링크: [https://github.com/hcgo97/leetcode/tree/master/0125-valid-palindrome](https://github.com/hcgo97/leetcode/tree/master/0125-valid-palindrome)_
- _링크: [https://leetcode.com/problems/valid-palindrome](https://leetcode.com/problems/valid-palindrome)_

> ### 문제 설명
>
> 모든 대문자를 소문자로 변환하고 영숫자가 아닌 문자를 모두 제거한 후 앞뒤가 같은 문구를 팰린드롬이라고 합니다. 영숫자 문자는 문자와 숫자를 포함합니다.

> 문자열 s가 주어지면 팰린드롬이면 참을 반환하고, 그렇지 않으면 거짓을 반환합니다.
> 
> ### **Example 1:**
> 
> - **Input:**
>   - `s = "A man, a plan, a canal: Panama"`
>
> - **Output:**
>   - `true`
>  
> - **Explanation:**
>   - `"amanaplanacanalpanama"` 은 팰린드롬 입니다.
> 
> ### **Example 2:**
> 
> - **Input:**
>   - `s = "race a car"`
> 
> - **Output:**
>   - `false`
>  
> - **Explanation:**
>   - `"raceacar"` 은 팰린드롬 입니다.
>  
> ### **Example 3:**
> 
> - **Input:**
>   - `s = " "`
> 
> - **Output:**
>   - `true`
>  
> - **Explanation:**
>   - `s`는 영숫자가 아닌 문자를 제거한 후 빈 문자열 `""`입니다.
>   - 빈 문자열은 앞뒤로 똑같이 읽히므로 팰린드롬입니다.
> 
> ### **Constraints:**
>
> - `1 <= s.length <= 2 * 10^5`
> - `s` 는 출력 가능한 ASCII 문자로만 구성됩니다.
>
<br></br>

## 풀이 과정

1. 문자열의 띄워쓰기, 특수문자를 모두 제거한다. 특수문자 제거는 파이썬의 re 라이브러리를 사용하여 정규식으로 처리하였다.
    ```python
    s = re.sub(r'[_\W]', '', s)
    ```
    
2. 문자열을 소문자로 변환한다.
    ```python
    s = s.lower()
    ```

3. 문자열을 다른 변수로 복사한 후, 거꾸로 뒤집는다.
    ```python
    sReverse = s[::-1]
    ```

4. 원본 문자열과 뒤집은 문자열이 같은지 비교한다.
    ```python
    if s == sReverse:
        return True
    else:
        return False
    ```
<br></br>

## 최초 제출 코드
```python
import re

class Solution(object):
    def isPalindrome(self, s):
        
        # 1. 문자열 띄워쓰기, 특수문자 없애기
        s = re.sub(r'[_\W]', '', s)
        
        # 2. 문자열 소문자로 변환
        s = s.lower()
        
        # 3. 변수 하나 더 만들고 뒤집기
        sReverse = s[::-1]
        
        # 4. 원본 문자열과 뒤집힌 원본 문자열이 똑같은지 비교
        if s == sReverse:
            return true
        else:
            return false
```
<br></br>

## 1차 수정

1. 문자열 특수문자 제거, 소문자로 변환하는 작업을 한번에 하도록 수정하였다.
    ```python
    s = re.sub(r'[_\W]', '', s).lower()
    ```

2. 뒤집은 문자열을 변수에 할당하지 않고 조건문에서 바로 비교하도록 하여 코드를 간결하게 하였다.
    ```python
    if s == s[::-1]:
        return True
    else:
        return False
    ```
<br></br>

## 최종 제출 코드
```python
import re

class Solution(object):
    def isPalindrome(self, s):
        
        # 1. 문자 특수문자 제거 및 소문자로 변환
        s = re.sub(r'[_\W]', '', s).lower()
        
        # 2. 원본 문자열과 뒤집힌 원본 문자열이 똑같은지 비교
        if s == s[::-1]:
            return True
        else:
            return False
```
<br></br>

## 시간, 공간 복잡도

### 시간 복잡도: `O(n)`
- 문자열의 특수문자 제거 및 소문자 변환하는 작업에는 문자열의 길이만큼의 시간이 소요되므로 `O(n)` 의 시간 복잡도를 가진다.
- 원본 문자열과 뒤집힌 원본 문자열이 같은지 비교하는 작업에는 문자열의 길이만큼의 시간이 소요되므로 마찬가지로 `O(n)` 의 시간 복잡도를 가진다.

### 공간 복잡도: `O(n)`
- 문자열의 특수문자 제거 작업과 소문자로 변환하는 작업에서 각각 새로운 문자열이 저장되므로 `O(1)` 의 공간 복잡도를 가진다.
<br></br>


## 문제 풀이 기록

![hyoj leet code submit history](img1.png "hyoj leet code submit history")
<br></br>

## 다른 풀이 방법

### 1. `isalnum()` 함수를 사용하는 방법 (시간: `O(n)`, 공간: `O(n)`)
- _*링크:* https://leetcode.com/problems/valid-palindrome/discuss/350929/Solution-in-Python-3-(beats-~100)-(two-lines)-(-O(1)-solution-as-well-)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # 1. 문자열을 소문자로 변환하고 알파벳과 숫자만을 선택하여 리스트를 생성한다.
        s = [i for i in s.lower() if i.isalnum()]
        
        # 2. 리스트 s 와 그 뒤집은 버전을 비교하여 팰린드롬 인지 여부를 확인한다.
        return s == s[::-1]
```

### 2. 투 포인터를 사용하는 방법 (시간: `O(n)`, 공간: `O(n)`)
- _*링크:* https://leetcode.com/problems/valid-palindrome/discuss/2438656/Very-Easy-oror-100-oror-Fully-Explained-(Java-C%2B%2B-Python-JS-Python3)

```python
class Solution(object):
    def isPalindrome(self, s):
        # 1. 왼쪽과 오른쪽 포인터를 초기화하고 입력 문자열의 양 끝을 가리키게 한다.
        left, right = 0, len(s) - 1

        while left < right:
            # 2. 왼쪽 포인터를 오른쪽으로 이동하여 알파벳과 숫자를 가리키게 한다.
            while left < right and not s[left].isalnum():
                left += 1

            # 3. 비슷하게 오른쪽 포인터를 왼쪽으로 이동하여 알파벳과 숫자를 가리키게 한다.
            while left < right and not s[right].isalnum():
                right -= 1

            # 4. 두 문자가 같은지 확인한다.
            if s[left].lower() != s[right].lower():
                # 4-1. 만약 같지 않다면 문자열은 유효한 팰린드롬이 아니므로 false 를 반환한다.
                return False

            # 4-2. 같다면 다음 반복으로 넘어가기 위해 양 포인터를 이동하여 다음 알파벳이나 숫자를 가리키게 한다.
            left, right = left + 1, right - 1

        # 5. 반복문이 성공적으로 종료되면 문자열이 팰린드롬이라 할 수 있으므로 true 를 반환한다.
        return True
```

## 회고
_이번 문제는 파이썬을 더 잘 알았다면 더 잘 풀 수 있었을 것 같다._

_나는 정규식 라이브러리를 사용하여 문자열을 바꾼 후 비교하는 방법을 사용했는데, 다른 풀이 방법에는 특수문자를 제외한 문자열만 선택하는 함수인 `isalnum()` 를 사용하여 푸는 방법을 사용하고 있었다._

_또한 투 포인터 방법도 있었는데, 이 문제는 투 포인터 방법을 사용해도 `O(n)` 의 시간, 공간 복잡도가 나오므로 궂이 번거롭게 투 포인터 방법을 사용하지 않고 `isalnum()` 함수를 사용하는 방법이 더 간편하다고 생각이 든다._