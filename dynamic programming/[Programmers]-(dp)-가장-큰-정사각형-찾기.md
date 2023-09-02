## 문제 설명
1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)

예를 들어

1	2	3	4
0	1	1	1
1	1	1	1
1	1	1	1
0	0	1	0
가 있다면 가장 큰 정사각형은

1	2	3	4
0	1	1	1
1	1	1	1
1	1	1	1
0	0	1	0
가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다.


## 제한사항
- 표(board)는 2차원 배열로 주어집니다.
- 표(board)의 행(row)의 크기 : 1,000 이하의 자연수
- 표(board)의 열(column)의 크기 : 1,000 이하의 자연수
- 표(board)의 값은 1또는 0으로만 이루어져 있습니다.


## 풀이 방법
1. 표에서 1에 해당하는 경우, "위/아래/대각선 중에서 가장 작은 수 + 1"이 가장 큰 정사각형에 해당한다.
  - 점화식 : dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1 


## 소스코드
```c++
#include <vector>
#include <algorithm>    // min
#include <cmath>    // pow

using namespace std;

int solution(vector<vector<int>> board){
    int answer = 0;

    int Y = board.size();
    int X = board[0].size();
    if(board.size() == 1){
        return 1;
    }
    
    for(int y = 1; y < Y; y++){
        for(int x = 1; x < X; x++){
            int daegak = board[y-1][x-1];
            int up = board[y-1][x];
            int left = board[y][x-1];
            
            if(board[y][x] > 0){
                board[y][x] = min({daegak, up, left}) + 1;
            }

        }
    }
    
    for(int y = 0; y < Y; y++){
        auto it = max_element(board[y].begin(), board[y].end());
        answer = max(answer, *it);
    }
    
    answer = pow(answer, 2);
    return answer;
}
```