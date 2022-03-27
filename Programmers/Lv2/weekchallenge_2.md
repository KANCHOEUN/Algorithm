### 문제

[모음 사전](https://programmers.co.kr/learn/courses/30/lessons/84512)

<br>

### **풀이**

```cpp
#include <string>
#include <vector>
#include <cmath>
using namespace std;

int f(int idx, int alpha) {
    int result = 0, round = 5 - idx;

    for(int i = 1; i < round; i++) {
        result += pow(5, i);
    }

    return alpha + result * (alpha-1);
}

int solution(string word) {
    int answer = 0;

    string s = "AEIOU";

    for(int i = 0; i < word.size(); i++) {
        answer += f(i, s.find(word[i]) + 1);
    }

    return answer;
}
```

<br>

### **다른 사람과 풀이 비교**

1. 'A', 'E', 'I', 'O', 'U' 를 연속된 숫자로 치환하는 방법

   - **map** 이용

     ```cpp
     map<char, int> m;

     m['A'] = 1;
     m['E'] = 2;
     m['I'] = 3;
     m['O'] = 4;
     m['U'] = 5;

     cout << m['E']; // 2
     ```

2. 핵심 로직

   ```cpp
   int a = word.size();
   for(int i = 0, b = 1; i < word.size(); i++, b *= 5) {
       a += s.find(word[i]) * 781 / b; // 781 에서 5 제곱수로 나눔
   }
   ```

   - a의 초기값: 각 자릿수마다의 첫 글자를 나타냄
     - "A"
     - "AA"
     - "AAA"
       s의 인덱스 값이 0부터 시작 => s.find("A") 는 0
       따라서 a의 초기값을 word.size()로 설정해줌
