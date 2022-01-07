---
title:  "[프로그래머스] 입국심사"
excerpt: "이분탐색 분류의 Lv3 문제"

categories:
  - Algorithm
tags:
  - Programmers
comments: false
last_modified_at: 2021-01-22T18:00:00
---
### 문제 설명
n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
- 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
- 심사관은 1명 이상 100,000명 이하입니다.

---
### 풀이
**30분**  
예전에 풀었지만 기억은 나지 않는 문제였는데, 다시 풀어도 풀이가 똑같았다. 우선 문제 조건에서 1,000,000,000명을 심사관 1명이 1,000,000,000분을 심사하는 경우를 생각했다. 그러면 10^12 의 시간이 걸리는데, 이것이 long long 범위인 2^63 - 1의 범위 안에 들어가는 것을 확인했다. 이진탐색을 구현하고 테스트코드를 통과해서 제출했는데, 줄줄이 실패했다.
```java
long long right = 1000000000 * n;
```
위의 코드에서 실수를 했었다. right가 long long 형이더라도 등호 오른쪽 식은 (int)*(int)의 형태이므로 원하는대로 작동하지 않았던 것이다. 그리고 중간값을 구하는 과정을 고치는 것이 좋아보인다.
```java
// mid = (left + right)/2;
mid = left + (right-left)/2;
```
경우에따라 left + right가 자료형의 최대 범위를 넘어 오버플로우를 발생시킬 수 있기 때문이다. 전혀 신경쓰지 않은 부분인데, 문제에 따라 중요한 부분이 될 수 있겠다는 생각이 들었다.

### 코드
```c++
// 11:11 ~ 11:43
#include <string>
#include <vector>

using namespace std;

long long solution(int n, vector<int> times) {
    long long left = 0;
    long long right = 1000000000 * (long long)n;
    long long mid, sum;
    
    while(left < right){
        mid = (left + right)/2;
        sum = 0;
        for(int time : times) sum += mid / (long long)time;
        
        if(sum >= n) right = mid;
        else left = mid + 1;
    }
    
    return right;
}
```

### 예전 코드
```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

long long solution(int n, vector<int> times) {
    long long ans = 0, min, max, mid;
    long long cnt;
    sort(times.begin(), times.end());
    min = 1;
    max = times[times.size()-1] * (long long)n;
    ans = max;
    while(min < max){
        mid = (min+max)/2;
        cnt = 0;
        for(auto t : times) cnt += mid/t;
        
        if(n <= cnt){
            max = mid-1;
            ans = mid;
        }
        else min = mid + 1;
    }
    return ans;
}
```