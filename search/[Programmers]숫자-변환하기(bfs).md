## 문제 설명
자연수 x를 y로 변환하려고 합니다. 사용할 수 있는 연산은 다음과 같습니다.

- x에 n을 더합니다
- x에 2를 곱합니다.
- x에 3을 곱합니다.

자연수 x, y, n이 매개변수로 주어질 때, x를 y로 변환하기 위해 필요한 최소 연산 횟수를 return하도록 solution 함수를 완성해주세요. 이때 x를 y로 만들 수 없다면 -1을 return 해주세요.


## 제한사항
- 1 ≤ x ≤ y ≤ 1,000,000
- 1 ≤ n < y


## 풀이방법
1. 3가지 연산(x+n, 2x, 3x)이 각 단계별로 동일하게 계산이 되는 규칙이 있으므로, 트리 형태의 계산구조를 가지고 있다.
2. 트리 형태의 계산구조에서 y로 만들 수 있는 경우의 수를 탐색한다. (`dfs` 또는 `bfs`)
   - 2가지 경우 전체 트리 검색 시 동일한 시간복잡도를 가지고 있으나,
   - 트리 일부 검색 시에는 tree depth가 짧은 경우에 dfs, tree branch가 적은 경우에는 bfs를 사용하는 것이 유리하다.
   - 이 문제는 tree depth(최대 1,000,000)보다 tree branch(3가지 경우)가 적기 때문에 bfs를 사용한다.
3. 일반적인 bfs를 적용할 경우, 중복되는 계산이 존재하여 시간초과 문제가 발생할 수 있으므로, 중복 계산을 제거한다. (중요!)


## 소스코드
```c++
#include <string>
#include <vector>
#include <queue>    // queue

using namespace std;

int answer = -1;
bool visited[1000001] = {false, };

void bfs(int x, int y, int n){
    queue<pair<int, int>> q;    // x, level
    q.push({x, 0});
    visited[x] = true;
    
    if(x == y){
        answer = 0;
        return ;
    }
    
    while(!q.empty()){
        int cx = q.front().first;
        int clevel = q.front().second;
        q.pop();
        
        if((cx + n == y) || (cx * 2) == y || (cx * 3) == y){
            answer = clevel + 1;
            break;
        }
        
        vector<int> nexts;
        nexts.push_back(cx + n);
        nexts.push_back(cx * 2);
        nexts.push_back(cx * 3);
        
        for(auto next : nexts){
            if(visited[next] == false && next < y){
                q.push({next, clevel + 1});
                visited[next] = true;
            }
        }
    }
}

int solution(int x, int y, int n) {
    bfs(x, y, n);
    return answer;
}
```