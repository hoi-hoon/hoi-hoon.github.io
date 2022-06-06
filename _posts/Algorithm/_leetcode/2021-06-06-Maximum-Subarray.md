---
title:  "[LeetCode] 53. Maximum Subarray"
excerpt: "Midium"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false
use_math: true
last_modified_at: 2021-06-06T12:00:00
---
### 문제 설명
[https://leetcode.com/problems/maximum-subarray](https://leetcode.com/problems/maximum-subarray/)
  
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.  
  
A subarray is a contiguous part of an array.  

### 제한사항
- 1 <= nums.length <= $10^5$
- $-10^4$ <= nums[i] <= $10^4$
  
---
### 풀이
**20분**  
릿코드에 구간합 관련 문제가 있나 검색해서 풀어보았다. 구간합을 계산할 때 이전 인덱스에서의 누적합이 음수라면 해당 인덱스부터 다시 구간합을 구하는 방식으로 최댓값을 갱신하면서 풀이하였다.  

```
Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```

### 코드
```c++
// 02:42 ~ 03:00
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = nums[0];
        int prefix_sum = nums[0];
        for(int i =1; i < nums.size(); ++i){
            if(prefix_sum > 0){
                prefix_sum += nums[i];
            } else {
                prefix_sum = nums[i];
            }
            
            if(prefix_sum > ans) ans = prefix_sum;
        }
        return ans;
    }
};
```