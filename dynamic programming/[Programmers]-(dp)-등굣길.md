## 문제 설명
계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.

가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.

격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다. 오른쪽과 아래쪽으로만 움직여 집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.


## 제한사항
- 격자의 크기 m, n은 1 이상 100 이하인 자연수입니다.
   - m과 n이 모두 1인 경우는 입력으로 주어지지 않습니다.
- 물에 잠긴 지역은 0개 이상 10개 이하입니다.
- 집과 학교가 물에 잠긴 경우는 입력으로 주어지지 않습니다.


## 풀이 방법
1. DP 점화식 : dp[y][x] = dp[y-1][x] + dp[y][x-1]
   - y == 0 인 경우 : dp[y][x] = dp[y][x-1]
   - x == 0 인 경우 : dp[y][x] = dp[y-1][x]


## 소스코드
```c++
#include <string>
#include <vector>

using namespace std;

int solution(int m, int n, vector<vector<int>> puddles) {
    int answer = 0;
    
    int matrix[n][m];
    fill(&matrix[0][0], &matrix[0][0] + (m * n), 0);
    
    bool visited[n][m];
    fill(&visited[0][0], &visited[0][0] + (m * n), false);
    
    for(auto e : puddles){
        matrix[e[1] - 1][e[0] - 1] = 0;
        visited[e[1] - 1][e[0] - 1] = true;
    }
    
    for(int y = 0; y < n; y++){
        for(int x = 0; x < m; x++){
            if(visited[y][x] == true){
                continue;
            }
            
            if(y == 0 && x == 0){
                matrix[y][x] = 1;
                visited[y][x] = true;
                continue;
            }
            
            if(y == 0){
                matrix[y][x] = matrix[y][x-1];
                visited[y][x] = true;
                continue;
            }
            
            if(x == 0){
                matrix[y][x] = matrix[y-1][x];
                visited[y][x] = true;
                continue;
            }
            
            matrix[y][x] = (matrix[y][x-1] + matrix[y-1][x]) % 1000000007;
            visited[y][x] = true;
        }
    }
    
    answer = matrix[n-1][m-1];
    return answer;
}
```