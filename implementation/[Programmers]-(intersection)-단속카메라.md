## 문제 설명
고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.

고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.


## 제한사항
- 차량의 대수는 1대 이상 10,000대 이하입니다.
- routes에는 차량의 이동 경로가 포함되어 있으며 routes[i][0]에는 i번째 차량이 고속도로에 진입한 지점, routes[i][1]에는 i번째 차량이 고속도로에서 나간 지점이 적혀 있습니다.
- 차량의 진입/진출 지점에 카메라가 설치되어 있어도 카메라를 만난것으로 간주합니다.
- 차량의 진입 지점, 진출 지점은 -30,000 이상 30,000 이하입니다.


## 문제 풀이
1. 차량 경로의 끝지점을 기준으로 차량 경로의 시작지점이 작은 경우를 찾으면,
   해당 끝지점으로 커버할 수 있는 차량 경로를 계산할 수 있다.


## 소스코드
```c++
#include <string>
#include <vector>
#include <algorithm>    // sort

using namespace std;

int solution(vector<vector<int>> routes) {
    int answer = 0;
    
    sort(routes.begin(), routes.end(), [](auto a, auto b){
        return a[1] < b[1];
    });
    
    int index = 0;
    int camera = routes[0][1];
    answer++;
    while(index < routes.size()){
        if(routes[index][0] <= camera){
            index++;
            continue;
        }
        
        camera = routes[index][1];
        answer++;
        index++;
    }
    
    return answer;
}
```