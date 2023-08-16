## 문제 설명
n명의 사람이 일렬로 줄을 서고 있습니다. n명의 사람들에게는 각각 1번부터 n번까지 번호가 매겨져 있습니다. n명이 사람을 줄을 서는 방법은 여러가지 방법이 있습니다. 예를 들어서 3명의 사람이 있다면 다음과 같이 6개의 방법이 있습니다.

[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]

사람의 수 n과, 자연수 k가 주어질 때, 사람을 나열 하는 방법을 사전 순으로 나열 했을 때, k번째 방법을 return하는 solution 함수를 완성해주세요.


## 제한사항
- n은 20이하의 자연수 입니다.
- k는 n! 이하의 자연수 입니다.


## 풀이 방법
1. 모든 경우의 수에 대해서 계산하는 방법의 최악의 경우는 O(n!)이므로, 사용이 불가능하다.
2. k번째 나열 방법을 계산하는 식을 사용한다.
  - 0번째 자리 : (k-1) / (n-1)! 번째의 작은 수
  - 1번째 자리 : 이전 계산식의 나머지 / (n-2)! 번째의 작은 수
  - ... 로 계산한다.


## 소스코드
```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int n, long long k) {
    vector<int> answer;
    
    long long dp[21];
    dp[0] = 1; dp[1] = 1;
    for(int i = 2; i <= n; i++){
        dp[i] = i * dp[i-1];
    }
    
    vector<bool> visited(n, false);
    k = k - 1;
    for(int i = n - 1; i >= 0; i--){
        int index = k / dp[i];
        for(int j = 0; j < n; j++){
            if(visited[j] == true){
                continue;
            }
            
            if(index > 0){
                index--;
                continue;
            }
            
            answer.push_back(j+1);
            visited[j] = true;
            break;
        }
        
        k = k % dp[i];
    }
    
    return answer;
}
```