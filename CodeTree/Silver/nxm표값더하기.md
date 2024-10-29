## 문제

[n x m 표 값 더하기](https://www.codetree.ai/training-field/search/problems/add-n-x-m-table-values/description)

## 풀이

누적 합을 활용하여 O(1) 시간복잡도로 좌상단 좌표가 (x1, y1)이고, 우하단 좌표가 (x2, y2)인 직사각형 내 값들의 합을 구하는 문제

```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder("");
        String[] s = br.readLine().split(" ");

        int n = Integer.parseInt(s[0]);
        int m = Integer.parseInt(s[1]);
        int[][] board = new int[n+1][m+1];
        int[][] d = new int[n+1][m+1];
        for (int i = 1; i <= n; i++) {
            String[] row = br.readLine().split(" ");
            for (int j = 1; j <= m; j++) {
                board[i][j] = Integer.parseInt(row[j-1]);
                d[i][j] = d[i-1][j] + d[i][j-1] - d[i-1][j-1] + board[i][j];
            }
        }
        
        int k = Integer.parseInt(br.readLine());
        for (int i = 0; i < k; i++) {
            String[] square = br.readLine().split(" ");
            int x1 = Integer.parseInt(square[0]);
            int y1 = Integer.parseInt(square[1]);
            int x2 = Integer.parseInt(square[2]);
            int y2 = Integer.parseInt(square[3]);
            sb.append((d[x2][y2] - d[x1-1][y2] - d[x2][y1-1] + d[x1-1][y1-1]) + "\n");
        }

        System.out.println(sb.toString());
    }
}
```