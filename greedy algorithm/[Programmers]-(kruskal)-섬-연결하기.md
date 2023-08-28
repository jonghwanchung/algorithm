## 문제 설명
n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.


## 제한사항
- 섬의 개수 n은 1 이상 100 이하입니다.
- costs의 길이는 ((n-1) * n) / 2이하입니다.
- 임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
- 같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
- 모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
- 연결할 수 없는 섬은 주어지지 않습니다.


## 풀이 방법
1. n개의 섬을 최소 비용으로 연결하는 MST를 구하는 문제이므로, `kruskal 알고리즘`을 사용한다.
  - 모든 edge를 cost/weight 기준으로 `non-decreasing order`로 정렬한다. (`sort`)
  - 모든 node를 `disjoint-set`으로 구성한다.
  - 낮은 cost/weight를 시작으로 disjoint-set을 연결한다.


## 소스코드
```c++
#include <string>
#include <vector>
#include <algorithm>    // sort

using namespace std;

int parents[101];

int root(int a){
    return (parents[a] == a) ? a : root(parents[a]); 
}

void unionSet(int a, int b){
    int aroot = root(a), broot = root(b);
    parents[broot] = aroot;
}

int solution(int n, vector<vector<int>> costs) {
    int answer = 0;
    
    sort(costs.begin(), costs.end(), [](auto a, auto b){
        return a[2] < b[2];
    });
    
    for(int i = 0; i < n; i++){
        parents[i] = i;
    }
    
    for(auto e : costs){
        int a = e[0], b = e[1];
        if(root(a) != root(b)){
            unionSet(a, b);
            answer += e[2];
        }
    }
    
    return answer;
}
```