## 문제 설명
호텔을 운영 중인 코니는 최소한의 객실만을 사용하여 예약 손님들을 받으려고 합니다. 한 번 사용한 객실은 퇴실 시간을 기준으로 10분간 청소를 하고 다음 손님들이 사용할 수 있습니다.
예약 시각이 문자열 형태로 담긴 2차원 배열 book_time이 매개변수로 주어질 때, 코니에게 필요한 최소 객실의 수를 return 하는 solution 함수를 완성해주세요.


## 제한사항
- 1 ≤ book_time의 길이 ≤ 1,000
   - book_time[i]는 ["HH:MM", "HH:MM"]의 형태로 이루어진 배열입니다
      - [대실 시작 시각, 대실 종료 시각] 형태입니다.
- 시각은 HH:MM 형태로 24시간 표기법을 따르며, "00:00" 부터 "23:59" 까지로 주어집니다.
   - 예약 시각이 자정을 넘어가는 경우는 없습니다.
   - 시작 시각은 항상 종료 시각보다 빠릅니다.


## 풀이 방법
1. 대실 종료 시간을 기준으로 오름차순으로 정렬한다. (`sort`)
2. 대실 시작 시간이 대실 종료 시간(+ 청소시간 포함)보다 작은 객실을 찾는다. (`중첩된 객실`을 찾을 수 있음)


## 소스코드
```c++
#include <string>
#include <vector>
#include <algorithm>    // sort, count_if
#include <cmath>    // max

using namespace std;

struct customer{
    int s, e;
};

int getTime(string time){
    string hour = time.substr(0, 2);
    string min = time.substr(3, 2);
    return (stoi(hour) * 60) + stoi(min);
}

int solution(vector<vector<string>> book_time) {
    int answer = 0;
    
    vector<customer> v;
    for(auto e : book_time){
        v.push_back({getTime(e[0]), getTime(e[1]) + 10});
    }
    
    sort(v.begin(), v.end(), [](auto a, auto b){
        return a.e < b.e;
    });
    
    for(int i = 0; i < v.size(); i++){
        int base = v[i].e;
        int cnt = count_if(v.begin() + i + 1, v.end(), [base](auto a){
            return a.s < base;
        });
        
        answer = max(answer, cnt + 1);
    }
    
    return answer;
}
```