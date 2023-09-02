---
title:  "[LeetCode] 36. Valid Sudoku"
excerpt: "top-interview-150"

categories:
  - Algorithm
tags:
  - LeetCode
comments: false 
use_math: true
last_modified_at: 2023-09-02T00:00:00
---
### 문제 설명
[https://leetcode.com/problems/valid-sudoku/](https://leetcode.com/problems/valid-sudoku/)


---
### 풀이
**20분**  
10분 정도 풀이법을 고민하다, 마땅히 효율적인 코드가 생각이 안 나서 냅다 풀었다. 제출한 이후 다른 사람의 코드를 참조하여 다시 풀이했다... 해시맵을 활용한 풀이를 떠올리긴 했지만, 배열의 차원을 높여서 행과 열을 나눠 기록할 생각까지는 닿지 못해서 아쉽다.

### 코드
```c++
// 14:22 ~ 14:43
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int count[10];

        for(int i = 0; i < 9; ++i){
            memset(count, 0, sizeof(count));
            for(int j = 0; j < 9; ++j){
                if(board[i][j] != '.'){
                    count[board[i][j] - '0'] += 1;
                    if(count[board[i][j] - '0']  > 1) return false;
                }
            }
        }

        for(int j = 0; j < 9; ++j){
            memset(count, 0, sizeof(count));
            for(int i = 0; i < 9; ++i){
                if(board[i][j] != '.'){
                    count[board[i][j] - '0'] += 1;
                    if(count[board[i][j] - '0']  > 1) return false;
                }
            }
        }
        
        for(int i = 0; i < 9; i += 3){
            for(int j = 0; j < 9; j += 3){
                memset(count, 0, sizeof(count));
                for(int di = 0; di < 3; ++di){
                    for(int dj = 0; dj < 3; ++dj){
                        if(board[i + di][j + dj] != '.'){
                            count[board[i + di][j + dj] - '0'] += 1;
                            if(count[board[i + di][j + dj] - '0']  > 1) return false;
                        }
                    }
                }
            }
        }

        return true;
    }
};
```

### 다른 코드
```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int row[9][10] = {0,};
        int col[9][10] = {0,};
        int box[3][3][10] = {0,};

        for(int i = 0; i < 9; ++i){
            for(int j = 0; j < 9; ++j){
                if(board[i][j] == '.') continue;
                int n = board[i][j] - '0';
                
                row[i][n] += 1;
                if(row[i][n] > 1) return false;
                
                col[j][n] += 1;
                if(col[j][n] > 1) return false;

                box[i/3][j/3][n] += 1;
                if(box[i/3][j/3][n] > 1) return false;
            }
        }
        return true;
    }
};
```