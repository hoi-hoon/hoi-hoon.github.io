---
title:  "[LeetCode] Remove Duplicates from Sorted Array"
excerpt: "top-interview-questions-easy"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2021-07-03T12:00:00
---
### 문제 설명
[https://leetcode.com/problems/remove-duplicates-from-sorted-array/](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
  
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

### 제한사항
- Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory. 
- 1 <= nums.length <= 3 * $10^4$
- -100 <= nums[i] <= 100
- nums is sorted in non-decreasing order

---
### 풀이
**10분**  
in-place 형태로 배열의 중복 원소를 제거하는 문제였다.  
가장 vote를 많이 받은 답안을 보니, 굳이 swap하지 않아도 되었다는 걸 깨달았다..
```c++
int count = 0;
for(int i = 1; i < n; i++){
    if(A[i] == A[i-1]) count++;
    else A[i-count] = A[i];
}
return n-count;
```

### 코드
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 0;
        for(int i = 1; i < nums.size(); ++i){
            if(nums[i] > nums[k]){
                int temp = nums[k + 1];
                nums[k + 1] = nums[i];
                nums[i] = temp;
                ++k;
            }
        }
        return k + 1;
    }
};
```

### 수정한 코드
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 0;
        for(int i = 1; i < nums.size(); ++i){
            if(nums[i] > nums[k]){
                k += 1;
                nums[k] = nums[i];
            }
        }
        return k + 1;
    }
};
```