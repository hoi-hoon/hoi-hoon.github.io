---
title:  "[LeetCode] remove-duplicates-from-sorted-array-ii"
excerpt: "top-interview-150"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2023-08-24T12:00:00
---
### 문제 설명
[https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)


---
### 풀이
**10분**  
정렬된 배열을 순회하면서, 같은 숫자가 최대 2번까지만 중복되도록 그 이상의 중복은 삭제하도록 했다.  
vector의 erase 메소드는 매우 비효율적이므로, 다소 무식한(?) 풀이법이였다. index 혹은 count 변수를 선언해서 배열 크기를 찾아가는 방식이 더 나아보인다.


### 코드
```c++
// 10:30 ~ 10:41

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        for (int i = 1; i < nums.size(); ++i){
            if(nums[i] == nums[i - 1] && i + 1 < nums.size()){
                while(i + 1 < nums.size() && nums[i] == nums[i + 1]){
                    nums.erase(nums.begin() + i + 1);
                }
            }
        }
        return nums.size();
    }
};
```

### 다른 코드
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n =nums.size();
        if(n < 3) return n;
        
        int indx = 2;
        for(int i =2; i< nums.size(); i++){
             if(nums[i] != nums[indx -2]){
                 nums[indx] = nums[i];
                 indx++;
             }
        }
        return indx;
  }
};
```