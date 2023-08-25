---
title:  "[LeetCode] 167. Two Sum II - Input Array Is Sorted"
excerpt: "top-interview-150"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2023-08-25T00:00:00
---
### 문제 설명
[https://leetcode.com/problems/two-sum-ii-input-array-is-sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)


---
### 풀이
**20분**  
'정렬된 배열'에 꽂혀서인지, 이분탐색 풀이를 처음에 떠올리고 고민했다. 내부적으로 이분탐색을 이용하는 lower_bound() 함수를 이용하여 더해서 target **이상**이 될 수 있는 값의 인덱스를 찾고, 더해서 정확히 target 값이 되는지 판단했다. 더하는 값의 인덱스가 중복되면 안 된다는 조건을 간과하여 한 번에 통과하지는 못했다.  
사실 이분탐색이 아니라 two pointer 방식으로 접근했다면 훨씬 간단하고 효율적으로 풀이했을 것 같다.


### 틀린 코드
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        for(int i = 0; i < numbers.size(); ++i){
            int j = lower_bound(numbers.begin(), numbers.end(), target - numbers[i]) - numbers.begin();
            if(numbers[i] + numbers[j] == target){
                return vector<int> {i + 1, j + 1};
            }
        }
        return vector<int> {-1, -1};
    }
};
```

### 코드
```c++
// 10:10 ~ 10:30
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        for(int i = 0; i < numbers.size(); ++i){
            int j = lower_bound(numbers.begin() + i + 1, numbers.end(), target - numbers[i]) - numbers.begin();
            if(j < numbers.size() && numbers[i] + numbers[j] == target){
                return vector<int> {i + 1, j + 1};
            }
        }
        return vector<int> {-1, -1};
    }
};
```