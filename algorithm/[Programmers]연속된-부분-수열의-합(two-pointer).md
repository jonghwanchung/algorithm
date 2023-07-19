## 문제설명
**비내림차순**으로 정렬된 수열이 주어질 때, 다음 조건을 만족하는 부분 수열을 찾으려고 합니다.

- 기존 수열에서 임의의 **두 인덱스**의 원소와 그 사이의 원소를 모두 포함하는 부분 수열이어야 합니다.
- 부분 수열의 합은 k입니다.
- 합이 k인 부분 수열이 여러 개인 경우 **길이가 짧은 수열**을 찾습니다.
- 길이가 짧은 수열이 여러 개인 경우 **앞쪽(시작 인덱스가 작은)에 나오는 수열**을 찾습니다.

수열을 나타내는 정수 배열 sequence와 부분 수열의 합을 나타내는 정수 k가 매개변수로 주어질 때, 위 조건을
만족하는 부분 수열의 **시작 인덱스**와 **마지막 인덱스**를 배열에 담아 return 하는 solution 함수를 완성
해주세요. 이때 수열의 인덱스는 **0부터 시작**합니다.


## 제한사항
- 5 ≤ sequence의 길이 ≤ 1,000,000
   - 1 ≤ sequence의 원소 ≤ 1,000
   - sequence는 비내림차순으로 정렬되어 있습니다.

- 5 ≤ k ≤ 1,000,000,000
   - k는 항상 sequence의 부분 수열로 만들 수 있는 값입니다.


## 풀이방법(고민)
1. 문제의 설명 `그대로 구현`하는 방식
   - 원소의 갯수가 1..n에 대하여 sequence 배열의 1..n까지 부분 수열을 구한 후
   - 부분 수열의 원소합 = k인 경우를 찾을 때까지 탐색
```
이 방법의 시간복잡도를 간단하게 계산해보면, 최소 O(n²)이 걸리며
sequence의 길이가 최대 1,000,000이므로 제한시간 내에 수행이 불가능하다!
```

2. `투 포인터`(Two-pointer) 방식   ... **구현**
   - sequence 배열의 1..n 부분에서 첫번째 원소부터 1개의 부분 수열이라고 가정한다.
   - 이를 위해, 투 포인터를 start = 0, end = 0인 상태(원소합 = sequence[0])로 시작한다.
   - 비내림차순으로 정렬된 배열이 주어지기 때문에,
   - 부분 수열의 합이 k보다 작은 경우는 end 포인터의 인덱스를 +1 증가시키고,
   - 부분 수열의 합이 k보다 큰 경우는 start 포인터의 인덱스를 +1 증가시킨다.
   - 부분 수열의 합이 k인 경우는 solution에 해당하여 별도로 관리한다.
   - 최종적으로 solution 조건에 해당하는 값을 계산한다.


## 소스코드
```C++
#include <string>
#include <vector>
#include <algorithm> // sort

using namespace std;

vector<int> solution(vector<int> sequence, int k) {
    vector<int> answer;
    
    vector<pair<int, int>> v;
    
    long long sum = sequence[0];
    int start = 0, end = 0;
    while(end < sequence.size()){
        if(sum < k){
            end++;
            sum += sequence[end];
            continue;
        }
        
        if(sum == k){
            v.push_back({start, end});
        }
        sum -= sequence[start];
        start++;
    }
    
    sort(v.begin(), v.end(), [](auto a, auto b){
        int alen = a.second - a.first + 1;
        int blen = b.second - b.first + 1;
        if(alen == blen){
            return a.first < b.first;
        }
        return alen < blen;
    });
    
    answer.push_back(v[0].first);
    answer.push_back(v[0].second);
    return answer;
}
```
