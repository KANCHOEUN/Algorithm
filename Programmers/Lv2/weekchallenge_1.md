## 문제

[피로도](https://programmers.co.kr/learn/courses/30/lessons/87946)

<br/>

## 풀이

```cpp
#include <string>
#include <vector>
using namespace std;

int result = 0;
int visited[8] = {0, };

void f(int cnt, int k, vector<vector<int> > d) {
    if(result < cnt) result = cnt;

    for(int i = 0; i < d.size(); i++) {
        if(!visited[i] && d[i][0] <= k) {
            visited[i] = 1;
            f(cnt+1, k-d[i][1], d);
            visited[i] = 0;
        }
    }
}

int solution(int k, vector<vector<int>> dungeons) {
    f(0, k, dungeons);

    return result;
}
```

<br>

- DFS
  던전의 개수가 1 이상 8 이하로 DFS를 해도 무방함
  visited 배열을 둠으로써 재귀 호출 여부를 결정

- Backtracking
  던전을 탐험할 때 필요한 "최소 필요 피로도"가 유저의 "현재 피로도"보다 높은 경우,
  즉 최소 필요 피로도 > 유저의 피로도인 경우에는 던전 탐험 불가
  해당 조건으로 가지치기를 할 수 있음

<br>

### 다른 사람과 풀이 비교

```cpp
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

int solution(int k, vector<vector<int>> dungeons) {
    int answer = -1;
    vector<int> order;
    for (int i = 0; i < dungeons.size(); i++) {
        order.push_back(i);
    }
    do {
        int temp = k;
        int count = 0;
        for (auto k : order) {
            if (temp < dungeons[k][0]) {
                break;
            }
            temp -= dungeons[k][1];
            count++;
        }
        answer = max(answer, count);
    } while (next_permutation(order.begin(), order.end()));
    return answer;
}
```
