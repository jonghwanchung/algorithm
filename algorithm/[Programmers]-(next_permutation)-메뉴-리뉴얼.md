## 문제 설명
레스토랑을 운영하던 스카피는 코로나19로 인한 불경기를 극복하고자 메뉴를 새로 구성하려고 고민하고 있습니다.
기존에는 단품으로만 제공하던 메뉴를 조합해서 코스요리 형태로 재구성해서 새로운 메뉴를 제공하기로 결정했습니다. 어떤 단품메뉴들을 조합해서 코스요리 메뉴로 구성하면 좋을 지 고민하던 "스카피"는 이전에 각 손님들이 주문할 때 가장 많이 함께 주문한 단품메뉴들을 코스요리 메뉴로 구성하기로 했습니다.
단, 코스요리 메뉴는 최소 2가지 이상의 단품메뉴로 구성하려고 합니다. 또한, 최소 2명 이상의 손님으로부터 주문된 단품메뉴 조합에 대해서만 코스요리 메뉴 후보에 포함하기로 했습니다.

예를 들어, 손님 6명이 주문한 단품메뉴들의 조합이 다음과 같다면,
(각 손님은 단품메뉴를 2개 이상 주문해야 하며, 각 단품메뉴는 A ~ Z의 알파벳 대문자로 표기합니다.)

손님 번호	주문한 단품메뉴 조합
1번 손님	A, B, C, F, G
2번 손님	A, C
3번 손님	C, D, E
4번 손님	A, C, D, E
5번 손님	B, C, F, G
6번 손님	A, C, D, E, H

가장 많이 함께 주문된 단품메뉴 조합에 따라 "스카피"가 만들게 될 코스요리 메뉴 구성 후보는 다음과 같습니다.

코스 종류	메뉴 구성	설명
요리 2개 코스	A, C	1번, 2번, 4번, 6번 손님으로부터 총 4번 주문됐습니다.
요리 3개 코스	C, D, E	3번, 4번, 6번 손님으로부터 총 3번 주문됐습니다.
요리 4개 코스	B, C, F, G	1번, 5번 손님으로부터 총 2번 주문됐습니다.
요리 4개 코스	A, C, D, E	4번, 6번 손님으로부터 총 2번 주문됐습니다.


각 손님들이 주문한 단품메뉴들이 문자열 형식으로 담긴 배열 orders, "스카피"가 추가하고 싶어하는 코스요리를 구성하는 단품메뉴들의 갯수가 담긴 배열 course가 매개변수로 주어질 때, "스카피"가 새로 추가하게 될 코스요리의 메뉴 구성을 문자열 형태로 배열에 담아 return 하도록 solution 함수를 완성해 주세요.


## 제한사항
- orders 배열의 크기는 2 이상 20 이하입니다.
- orders 배열의 각 원소는 크기가 2 이상 10 이하인 문자열입니다.
   - 각 문자열은 알파벳 대문자로만 이루어져 있습니다.
   - 각 문자열에는 같은 알파벳이 중복해서 들어있지 않습니다.
- course 배열의 크기는 1 이상 10 이하입니다.
   - course 배열의 각 원소는 2 이상 10 이하인 자연수가 오름차순으로 정렬되어 있습니다.
   - course 배열에는 같은 값이 중복해서 들어있지 않습니다.
- 정답은 각 코스요리 메뉴의 구성을 문자열 형식으로 배열에 담아 사전 순으로 오름차순 정렬해서 return 해주세요.
   - 배열의 각 원소에 저장된 문자열 또한 알파벳 오름차순으로 정렬되어야 합니다.
   - 만약 가장 많이 함께 주문된 메뉴 구성이 여러 개라면, 모두 배열에 담아 return 하면 됩니다.
   - orders와 course 매개변수는 return 하는 배열의 길이가 1 이상이 되도록 주어집니다.


## 풀이 방법
1. 각 손님들이 주문한 단품메뉴들에서 코스요리를 구성하는 단품메뉴들의 갯수만큼 해당되는 조합(`combination`)을 구한다.
   - 제한사항에서 orders 배열의 크기가 최대 20이고, course 원소의 크기가 최소 2개이므로, 조합을 사용해도 무방하다.
2. 각 손님들이 주문한 단품메뉴들의 순서가 바뀌는 경우도 같은 경우에 해당되므로,
   자료구조(`set`)과 알고리즘(`sort`)을 사용하여 이를 처리한다.
3. 최소 2명 이상의 손님으로부터 주문된 단품메뉴 조합에 대해서만 코스요리 메뉴 후보를 포함하는 제약이 있으므로,
   발생한 조합의 수가 2개 이상인 경우에만 메뉴 후보에 포함한다.


## 소스코드
```c++
#include <string>
#include <vector>
#include <map>  // map
#include <set>  // set
#include <algorithm>    // sort, next_permutation, max_element

using namespace std;

vector<string> solution(vector<string> orders, vector<int> course) {
    set<string> s;
    
    for(auto k : course){
        map<string, int> m;
        for(auto o : orders){
            vector<bool> flags(o.size(), false);
            fill(flags.begin(), flags.begin() + k, true);
            sort(flags.begin(), flags.end());
            do{
                string combo = "";
                for(int i = 0; i < flags.size(); i++){
                    if(flags[i] == true){
                        combo += o[i];
                    }
                }
                sort(combo.begin(), combo.end());
                m[combo] += 1;
            }while(next_permutation(flags.begin(), flags.end()));
        }
        
        auto it = max_element(m.begin(), m.end(), [](auto a, auto b){
            return a.second < b.second;
        });
        
        int max = it->second;
        if(max < 2){
            continue;
        }
        for(auto e : m){
            if(e.second == max){
                s.insert(e.first);
            }
        }
    }
    
    vector<string> answer(s.begin(), s.end());
    sort(answer.begin(), answer.end());
    return answer;
}
```