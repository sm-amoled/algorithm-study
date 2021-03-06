# 이동하기

문제 번호: 11048
알고리즘 분류: DP
푼 날짜: 2021년 2월 21일 오후 9:50

## 문제링크

[https://www.acmicpc.net/problem/11048](https://www.acmicpc.net/problem/11048)

## 문제

준규는 N×M 크기의 미로에 갇혀있다. 미로는 1×1크기의 방으로 나누어져 있고, 각 방에는 사탕이 놓여져 있다. 미로의 가장 왼쪽 윗 방은 (1, 1)이고, 가장 오른쪽 아랫 방은 (N, M)이다.

준규는 현재 (1, 1)에 있고, (N, M)으로 이동하려고 한다. 준규가 (r, c)에 있으면, (r+1, c), (r, c+1), (r+1, c+1)로 이동할 수 있고, 각 방을 방문할 때마다 방에 놓여져있는 사탕을 모두 가져갈 수 있다. 또, 미로 밖으로 나갈 수는 없다.

준규가 (N, M)으로 이동할 때, 가져올 수 있는 사탕 개수의 최댓값을 구하시오.

## 입력

첫째 줄에 미로의 크기 N, M이 주어진다. (1 ≤ N, M ≤ 1,000)

둘째 줄부터 N개 줄에는 총 M개의 숫자가 주어지며, r번째 줄의 c번째 수는 (r, c)에 놓여져 있는 사탕의 개수이다. 사탕의 개수는 0보다 크거나 같고, 100보다 작거나 같다.

## 출력

첫째 줄에 준규가 (N, M)으로 이동할 때, 가져올 수 있는 사탕 개수를 출력한다.

## 조건

- 시간 제한 : 1s
- 메모리 제한 : 256MB

---

## 해설

(r, c)에 대해서는 (r-1, c), (r, c-1), (r-1, c-1)에서 접근할 수 있는데, 최대한 많은 방을 방문하는 것이 이득이므로 (r-1, c), (r, c-1)에서 접근하는 경우만 생각해주면 된다.

2차원 벡터를 만들어서, (1, 1) 에서 (M, N) 까지 가는 길에 있는 사탕의 합을 각 방에 대응하는 dp에 저장하면서 구하면 된다. 

## 풀이

(r-1, c-1)에 접근을 하기위해 왼쪽, 위쪽 면을 0으로 채워야 하기에, M, N을 입력받으면 M+1, N+1의 크기를 갖는 2차원 벡터를 만든다. 

```cpp
int M, N;
cin >> M >> N;

vector<vector<int>> dp(M+1, vector<int> (N+1, 0));
```

(i, j) 에 대해서는 dp(i-1, j), dp(i, j-1) 중 큰 값에 (i, j)에 있는 사탕 개수를 합하여 dp(i, j)의 값을 구할 수 있다. 이를 코드로 구현하면 아래처럼 작성할 수 있다.

```cpp
int input;
for(int i = 1; i <= M; i++) {
    for(int j = 1; j <= N; j++) {
        cin >> input;   
        dp[i][j] += (input + ((dp[i-1][j] > dp[i][j-1])? dp[i-1][j] : dp[i][j]; 
    }
}
```

위 반복문을 종료하고 나면, dp[M][N]에 원하는 결과가 담겨있다.

```cpp
cout << dp[M][N];
```

---

## 코멘트

이까지는 할 만 하지 ㅎㅎ

---

## 코드

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0); cout.tie(0);
    
    int M, N;
    cin >> M >> N;
    
    vector<vector<int>> dp(M+1, vector<int> (N+1, 0));
    
    int input;
    for(int i = 1; i <= M; i++) {
        for(int j = 1; j <= N; j++) {
            cin >> input;   
            dp[i][j] += (input + ((dp[i-1][j] > dp[i][j-1])? dp[i-1][j] : dp[i][j-1]));  
        }
    }
    
    cout << dp[M][N];
    return 0;
}
```