---
title:  "[프로그래머스] 징검다리"
excerpt: "이분탐색 분류의 Lv4 문제"

categories:
  - Algorithm
tags:
  - Programmers
  - failed
comments: false
last_modified_at: 2021-01-23T18:00:00
---
### 문제 설명
출발지점부터 distance만큼 떨어진 곳에 도착지점이 있습니다. 그리고 그사이에는 바위들이 놓여있습니다. 바위 중 몇 개를 제거하려고 합니다.
예를 들어, 도착지점이 25만큼 떨어져 있고, 바위가 [2, 14, 11, 21, 17] 지점에 놓여있을 때 바위 2개를 제거하면 출발지점, 도착지점, 바위 간의 거리가 아래와 같습니다.

| 제거한 바위의 위치	| 각 바위 사이의 거리	|거리의 최솟값|
| --- | --- | ---|
|[21, 17] |	[2, 9, 3, 11]|	2|
|[2, 21] | 	[11, 3, 3, 8]|	3|
|[2, 11] |	[14, 3, 4, 4]|	3|
|[11, 21] |	[2, 12, 3, 8]|	2|
|[2, 14] |	[11, 6, 4, 4]|	4|

위에서 구한 거리의 최솟값 중에 가장 큰 값은 4입니다.

출발지점부터 도착지점까지의 거리 distance, 바위들이 있는 위치를 담은 배열 rocks, 제거할 바위의 수 n이 매개변수로 주어질 때, 바위를 n개 제거한 뒤 각 지점 사이의 거리의 최솟값 중에 가장 큰 값을 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 도착지점까지의 거리 distance는 1 이상 1,000,000,000 이하입니다.
- 바위는 1개 이상 50,000개 이하가 있습니다.
- n 은 1 이상 바위의 개수 이하입니다.

---
### 풀이
**실패**  
이분 탐색으로 푸는 방법이 생각나지 않아서 다른 방법을 시도했지만, 시간이 오래 걸렸음에도 제대로된 풀이 방법이 생각나지 않아서 풀이를 찾아봤다. 내가 시도한 방법은 바위 사이의 거리를 구한 벡터를 선언하고, 벡터 원소의 위치와 값을 pair로 넣은 priority_queue를 이용해서 짧은 거리부터 지울 수 있도록 바위를 없애는 것 이었다. 그리고 바위를 없앨 때, 왼쪽과 오른쪽을 확인하여 더 작은 값과 합쳐주는 그리디한 방식으로 풀겠다는 계획을 세웠으나, 생각해보니 '더 작은 값과 합쳐주는'과정 때문에 불가능했다.
```
100  2  100  2  3 
```
위와 예시에서 4번째 값과 3번째 값을 합쳐주는 것이 맞지만, 최소값인 2는 중복되는데 2번째 값을 꺼낼 경우 애초에 그리디가 성립되지 않기 때문이다. 여기서 '그럼 앞, 뒤 값도 함께 저장해서 sort에 사용할까?'라는 생각을 했는데, 코드가 복잡해짐은 물론이고 점점 잘못되고 있다는 생각이 들었다.  
이분탐색 문제를 보고 이분탐색으로 풀어야하는 문제인지 눈치채는 것과, 그 풀이를 떠올리는 과정이 너무 미숙한 것 같다. 프로그래머스의 다른 이분탐색 문제를 풀어보면서 더 연습해야할 것 같다.

### 코드
```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int distance, vector<int> rocks, int n) {
    sort(rocks.begin(), rocks.end());
    int ans = 0;
    int left = 1,right = distance,mid;
    int sum,cnt;
    
    while(left <= right){
        mid = (left + right) / 2;
        cnt = 0;
        sum = 0;
        for(int i =0; i<rocks.size(); ++i){
            if(i==0){
                sum += rocks[i];
            }
            else sum += rocks[i] - rocks[i - 1];
            
            if(i == rocks.size() - 1){
                sum = min(sum, distance - rocks.back());
            }
            
            if(sum < mid){
                ++cnt;
            }
            else sum = 0;
            
            if(cnt > n) break;
        }
        
        if(cnt > n) right = mid - 1;
        else{
            ans = max(ans,mid);
            left = mid+1;
        }
    }
    return ans;
}
```