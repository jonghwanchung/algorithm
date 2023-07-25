## 문제 설명
땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. **1행부터** 땅을 밟으며 한 행씩 내려올 때, **각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다.** 단, 땅따먹기 게임에는 한 행씩 내려올 때, **같은 열을 연속해서 밟을 수 없는 특수 규칙**이 있습니다.

예를 들면,

| 1 | 2 | 3 | 5 |
| 5 | 6 | 7 | 8 |
| 4 | 3 | 2 | 1 |

로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.

마지막 행까지 모두 내려왔을 때, 얻을 수 있는 **점수의 최대값**을 return하는 solution 함수를 완성해 주세요. 위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.


## 제한사항
- 행의 개수 N : 100,000 이하의 자연수
- 열의 개수는 4개이고, 땅(land)은 2차원 배열로 주어집니다.
- 점수 : 100 이하의 자연수


## 풀이방법
1. 각 행(i)은 현재 값(x)에 이전 행(i-1)까지의 최대값(local optimum)을 누적하면, 마지막 행에서 4열의 최대값(global optimum)을 구할 수 있는 규칙이 있다. (`dynamic programming`)
  - land[i][0] = x + max(land[i-1][1], land[i-1][2], land[i-1][3])   ... i >= 1


## 소스코드
```C++
#include <iostream>
#include <vector>
#include <algorithm>    // max, max_element

using namespace std;

int solution(vector<vector<int> > land){
    int answer = 0;
    
    int Y = land.size();
    int X = land[0].size();
    
    int result[100001][4] = {0, };
    for(int x = 0; x < X; x++){
        result[0][x] = land[0][x];
    }
    
    for(int y = 1; y < Y; y++){
        result[y][0] = land[y][0] + max({result[y-1][1], result[y-1][2], result[y-1][3]});
        result[y][1] = land[y][1] + max({result[y-1][0], result[y-1][2], result[y-1][3]});
        result[y][2] = land[y][2] + max({result[y-1][0], result[y-1][1], result[y-1][3]});
        result[y][3] = land[y][3] + max({result[y-1][0], result[y-1][1], result[y-1][2]});
    }

    answer = *max_element(&result[Y-1][0], &result[Y-1][4]);
    return answer;
}
```