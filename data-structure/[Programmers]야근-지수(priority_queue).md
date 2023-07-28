## 문제 설명
회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. **야근 피로도**는 야근을 시작한 시점에서 **남은 일의 작업량**을 **제곱**하여 **더한 값**입니다. Demi는 N시간 동안 야근 피로도를 **최소화**하도록 일할 겁니다.Demi가 **1시간 동안 작업량 1만큼을 처리**할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.


## 제한 사항
- works는 길이 1 이상, 20,000 이하인 배열입니다.
- works의 원소는 50000 이하인 자연수입니다.
- n은 1,000,000 이하인 자연수입니다.


## 풀이 방법
1. 야근 피로도를 최소화하기 위해서는 남은 일의 작업량의 제곱을 줄여야 한다.
 => 남은 일의 작업량이 가장 큰 작업량을 우선적으로 처리한다.
2. 남은 일의 작업량이 가장 큰 작업량을 처리하기 위해 적절한 자료구조(`priority queue`)를 사용한다.
   - 매번 작업량 리스트(works)에서 가장 큰 작업량을 찾는 방법을 사용할 수도 있지만,
   - 이 방법의 시간 복잡도(수행시간)을 계산하면, #(works) * n = O(m * n) = 20,000 * 1,000,000 = 20,000,000,000 이므로 많은 연산이 발생하여 높은 시간 복잡도를 갖는다.
   - 반면에, 우선순위 큐(priority_queue)를 사용했을 때의 시간 복잡도를 계산하면, #(works) * O(log(n)) = O(m * log(n))이므로 상대적으로 낮은 시간 복잡도를 갖는다.


## 소스소스
```c++
#include <string>
#include <vector>
#include <queue>    // priority_queue
#include <cmath>    // pow

using namespace std;

long long solution(int n, vector<int> works) {
    long long answer = 0;
    
    priority_queue<int> pq; // max priority queue
    for(auto e : works){
        pq.push(e);
    }
    
    while(n > 0){
        auto m = pq.top();
        pq.pop();
        if(m == 0){
            return 0;
        }
        
        m -= 1;
        pq.push(m);
            
        n--;
    }
    
    while(!pq.empty()){
        answer += pow(pq.top(), 2);
        pq.pop();
    }
    
    return answer;
}
```