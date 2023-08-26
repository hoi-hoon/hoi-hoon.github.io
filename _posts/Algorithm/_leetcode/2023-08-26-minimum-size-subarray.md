---
title:  "[LeetCode] 209. Minimum Size Subarray Sum"
excerpt: "top-interview-150"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2023-08-26T00:00:00
---
### 문제 설명
[https://leetcode.com/problems/minimum-size-subarray-sum](https://leetcode.com/problems/minimum-size-subarray-sum)


---
### 풀이
**30분**  
two pointer 방식으로 풀이했다. 처음에 반복문 설계를 잘못해서, 조건문이 덕지덕지 붙는 것이 보기 싫어 고민해서 다시 작성했다.  
잘 이해가 안 되는 부분은, 문제의 분류가 sliding window 인데 two pointer 와의 차이점을 찾아보니 찾는 구간의 크기가 고정적이면 sliding window 라고 한다. 근데 문제는 최소 구간을 찾는 문제니, two pointer 로 보는게 맞지 않나...? 굳이 sliding window 로 풀려면 window size 를 1 ~ n 로 정해서 탐색해야 하는게 아닌가 싶다.

### 코드
```c++
// 15:32 ~ 16:00
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int min = 1000000001;
        int sum = nums[0];
        int i = 0, j = 0;
        while(j < nums.size()){
            if(sum < target){
                j += 1;
                if(j < nums.size()) sum += nums[j];
            } else {
                if(j - i + 1 < min) min = j - i + 1;
                sum -= nums[i];
                i += 1;
            }
        }
        if(min == 1000000001) return 0;
        return min;
    }
};
```