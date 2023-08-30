## 문제 설명
1 x 1 크기의 칸들로 이루어진 직사각형 격자 형태의 미로에서 탈출하려고 합니다. 각 칸은 통로 또는 벽으로 구성되어 있으며, 벽으로 된 칸은 지나갈 수 없고 통로로 된 칸으로만 이동할 수 있습니다. 통로들 중 한 칸에는 미로를 빠져나가는 문이 있는데, 이 문은 레버를 당겨서만 열 수 있습니다. 레버 또한 통로들 중 한 칸에 있습니다. 따라서, 출발 지점에서 먼저 레버가 있는 칸으로 이동하여 레버를 당긴 후 미로를 빠져나가는 문이 있는 칸으로 이동하면 됩니다. 이때 아직 레버를 당기지 않았더라도 출구가 있는 칸을 지나갈 수 있습니다. 미로에서 한 칸을 이동하는데 1초가 걸린다고 할 때, 최대한 빠르게 미로를 빠져나가는데 걸리는 시간을 구하려 합니다.

미로를 나타낸 문자열 배열 maps가 매개변수로 주어질 때, 미로를 탈출하는데 필요한 최소 시간을 return 하는 solution 함수를 완성해주세요. 만약, 탈출할 수 없다면 -1을 return 해주세요.


## 제한사항
- 5 ≤ maps의 길이 ≤ 100
   - 5 ≤ maps[i]의 길이 ≤ 100
   - maps[i]는 다음 5개의 문자들로만 이루어져 있습니다.
      - S : 시작 지점
      - E : 출구
      - L : 레버
      - O : 통로
      - X : 벽
   - 시작 지점과 출구, 레버는 항상 다른 곳에 존재하며 한 개씩만 존재합니다.
   - 출구는 레버가 당겨지지 않아도 지나갈 수 있으며, 모든 통로, 출구, 레버, 시작점은 여러 번 지나갈 수 있습니다.


## 풀이 방법
1. 시작지점(S)에서 레버(L)의 위치 찾는다. (`bfs`)
2. 레버(L)의 위치에서 출구(E)의 위치를 찾는다. (`bfs`)


## 소스코드
```c++
#include <string>
#include <vector>
#include <queue>

using namespace std;

struct node{
    int y, x;
    int dist;
};

int Y, X;

bool visited[101][101];

int dy[4] = {-1, 1, 0, 0};
int dx[4] = {0, 0, -1, 1};

int bfs(vector<string> maps, int y, int x, char target){
    fill(&visited[0][0], &visited[0][0] + (101 * 101), false);
    
    queue<node> q;
    q.push({y, x, 0});
    visited[y][x] = true;
    
    while(!q.empty()){
        int cy = q.front().y;
        int cx = q.front().x;
        int cdist = q.front().dist;
        q.pop();
        
        for(int i = 0; i < 4; i++){
            int ny = cy + dy[i];
            int nx = cx + dx[i];
            
            if(ny < 0 || ny >= Y || nx < 0 || nx >= X){
                continue;
            }
            
            if(visited[ny][nx] == true || maps[ny][nx] == 'X'){
                continue;
            }
            
            if(maps[ny][nx] == target){
                return cdist + 1;
            }
            
            q.push({ny, nx, cdist + 1});
            visited[ny][nx] = true;
        }
    }
    
    return 0;
}

int solution(vector<string> maps) {
    int answer = 0;
    
    Y = maps.size();
    X = maps[0].size();
    
    int sy = -1, sx = -1;
    int ly = -1, lx = -1;
    for(int y = 0; y < maps.size(); y++){
        auto it = maps[y].find('S');
        if(it != string::npos){
            sy = y; sx = it;
        }
        
        auto it2 = maps[y].find('L');

        if(it2 != string::npos){

            ly = y; lx = it2;

        }
    }
    
    int result = 0;
    result = bfs(maps, sy, sx, 'L');
    if(result == 0){
        return -1;
    }
    answer += result;
    
    result = bfs(maps, ly, lx, 'E');
    if(result == 0){
        return -1;
    }
    answer += result;
    
    return answer;
}
```