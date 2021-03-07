---
title:  "[LeetCode] 62. Unique Paths II"
excerpt: "Midium"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false
last_modified_at: 2021-03-04T12:00:00
---
### 문제 설명
https://leetcode.com/problems/unique-paths-ii/  
  
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).  
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).  
Now consider if some obstacles are added to the grids. How many unique paths would there be?  
  
An obstacle and space is marked as 1 and 0 respectively in the grid.

### 제한사항
- m == obstacleGrid.length
- n == obstacleGrid[i].length
- 1 <= m, n <= 100
- obstacleGrid[i][j] is 0 or 1.


---
### 풀이
**5분**  
Unique Paths I 문제는 매우 기초적인 문제였기에 따로 포스팅하지 않고, 이 문제만 포스팅하기로 했다.
영어 스크립트로 문제를 접하니 새로운 기분이 들었지만, 문제를 읽을수록 점점 익숙한 기분이 들었다. 프로그래머스 문제 중에서 풀이법이 같은 문제를 푼 적이 있는 것 같다.

### 코드
```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,0));
        
        for(int i = 0; i <m; ++i){
            if(obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for(int j = 0; j <n; ++j){
            if(obstacleGrid[0][j] == 1) break;
            dp[0][j] = 1;
        }
        for(int i = 1; i < m; ++i){
            for(int j = 1; j < n; ++j){
                if(obstacleGrid[i][j] != 1){
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }
};
```