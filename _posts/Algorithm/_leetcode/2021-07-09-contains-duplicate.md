---
title:  "[LeetCode] Contains Duplicate"
excerpt: "top-interview-questions-easy"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2021-07-09T12:00:00
---
### 문제 설명
[https://leetcode.com/problems/contains-duplicate/](https://leetcode.com/problems/contains-duplicate/)
  
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

### 제한사항
- 1 <= nums.length <= $10^5$
- -$10^9$ <= nums[i] <= $10^9$

---
### 풀이
**3분**  
배열 내부에서 중복이 발생했는지 판단하는 문제이다.  
처음에는 set 자료구조를 이용해서 풀이했다가, runtime performance 결과를 보고 unordered_set 자료구조로 변경하여 제출을 했었다.
그런데 그럼에도 배열을 정렬하여 중복을 찾아내는 풀이보다 속도가 떨어졌다. 정렬은 O(nlogn)인 반면, unodered_set은 hash를 사용하므로 상수시간 안에 삽입 및 접근이 가능한데도 이런 결과가 나온것은, **hash 연산에 소모되는 시간**때문인 것으로 생각된다. 아마 테스트케이스의 사이즈가 훨씬 컸다면 이 방법이 더 빠르지 않았을까..?? 

### 코드
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> s(nums.begin(), nums.end());
        if(nums.size() != s.size()) return true;
        return false;
    }
};
```
