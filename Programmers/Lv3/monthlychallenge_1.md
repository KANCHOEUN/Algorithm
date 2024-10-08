## 문제


## 풀이 

- 인접한 두 풍선 중 큰 번호 풍선을 터뜨린다.
- 단, 번호가 더 작은 풍선을 딱 한 번 터뜰리 수 있다.
- 풍선의 번호는 모두 다르다.

해당 문제는 문제의 예제를 보고 힌트를 얻을 수 있었다.

i번째 풍선이 가장 마지막에 남는 풍선이고,
번호가 더 작은 풍선을 가장 마지막 순서에 터뜨린다고 가정해보자.

i번째 풍선을 기준으로 좌측에 있는 값 하나(l)와 우측에 있는 값 하나(r)를 비교하고자 할 때,
- l 은 좌측 풍선들 중 최솟값,
- r 은 우측 풍선들 중 최솟값이어야 한다.

나올 수 있는 케이스는 다음과 같다.

1. l < a[i] 이고, a[i] < r 인 경우
2. l < a[i] 이고, a[i] > r 인 경우
3. l > a[i] 이고, a[i] < r 인 경우
4. l > a[i] 이고, a[i] > r 인 경우

- 1번의 경우, i번째 풍선 번호보다 작은 풍선인 l을 터뜨리고, i번째 풍선 번호보다 큰 풍선인 r을 터뜨리면 된다.
- 2번의 경우, l과 r 모두가 i번째 풍선보다 작은 풍선이므로 i번째 풍선은 마지막 풍선이 될 수 없다.
- 3번의 경우, l과 r 모두가 i번째 풍선보다 큰 풍선이므로 i번째 풍선은 마지막 풍선이 될 수 있다.
- 4번의 경우, i번째 풍선 번호보다 작은 풍선인 r을 터뜨리고, i번째 풍선 번호보다 큰 풍선인 l을 터뜨리면 된다.

따라서 2번의 케이스만 셈하지 않으면 된다.

그리고 index 번호가 `0`이거나 `a.length - 1` 인 경우, 좌측 or 우측 풍선들의 최솟값 번호가 어떤 값이 오든 최후까지 남기는 것이 가능한 풍선이다.

(+) 모두 다른 숫자이기 때문에 이는 다음과 같이 변경될 수 있다.

- `l[i]` : 0에서 i까지의 최솟값
- `r[i]` : n-1에서 i까지의 최솟값

1. l[i] != a[i] 이고, r[i] == a[i] 인 경우
2. l[i] != a[i] 이고, r[i] != a[i] 인 경우
3. l[i] == a[i] 이고, r[i] == a[i] 인 경우
4. l[i] == a[i] 이고, r[i] != a[i] 인 경우

2번의 케이스만 제외하고 셈하면 된다.

```java
import java.util.*;

class Solution {
    public int solution(int[] a) {
        int answer = 0;
        
        int N = a.length;
        int[] l = new int[N]; // 0에서 i까지의 최소
        int[] r = new int[N]; // n-1에서 i까지의 최소

        l[0] = a[0];
        r[N-1] = a[N-1];
        for (int i = 1; i < N; i++) {
            l[i] = Math.min(l[i-1], a[i]);
            r[N-i-1] = Math.min(r[N-i], a[N-i-1]);
        }
        
        for (int i = 0; i < N; i++) {
            boolean flag = true;
            if (l[i] != a[i] && r[i] != a[i]) flag = false;
            if (flag) answer++;
        }
        
        return answer;
    }
}
```


### 다른 사람 풀이

> l[i] != a[i] && r[i] != a[i]

위 식의 의미는 l[i] 혹은 r[i]를 구할 때, a[i]가 최솟값으로 변경되지 않는다는 뜻이다.

반대로 생각하면, 0부터 i까지의 최솟값이 a[i]이거나 N-1부터 i까지의 최솟값이 a[i]이면 된다.
즉 Math.min(...)이 변경될 때의 값들을 Set 자료구조에 기록하여 중복값을 방지하면서 세면 된다.