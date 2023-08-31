## 문제 설명
[본 문제는 정확성과 효율성 테스트 각각 점수가 있는 문제입니다.]

카카오는 하반기 경력 개발자 공개채용을 진행 중에 있으며 현재 지원서 접수와 코딩테스트가 종료되었습니다. 이번 채용에서 지원자는 지원서 작성 시 아래와 같이 4가지 항목을 반드시 선택하도록 하였습니다.

- 코딩테스트 참여 개발언어 항목에 cpp, java, python 중 하나를 선택해야 합니다.
- 지원 직군 항목에 backend와 frontend 중 하나를 선택해야 합니다.
- 지원 경력구분 항목에 junior와 senior 중 하나를 선택해야 합니다.
- 선호하는 소울푸드로 chicken과 pizza 중 하나를 선택해야 합니다.

인재영입팀에 근무하고 있는 니니즈는 코딩테스트 결과를 분석하여 채용에 참여한 개발팀들에 제공하기 위해 지원자들의 지원 조건을 선택하면 해당 조건에 맞는 지원자가 몇 명인 지 쉽게 알 수 있는 도구를 만들고 있습니다.
예를 들어, 개발팀에서 궁금해하는 문의사항은 다음과 같은 형태가 될 수 있습니다.
코딩테스트에 java로 참여했으며, backend 직군을 선택했고, junior 경력이면서, 소울푸드로 pizza를 선택한 사람 중 코딩테스트 점수를 50점 이상 받은 지원자는 몇 명인가?

물론 이 외에도 각 개발팀의 상황에 따라 아래와 같이 다양한 형태의 문의가 있을 수 있습니다.

- 코딩테스트에 python으로 참여했으며, frontend 직군을 선택했고, senior 경력이면서, 소울푸드로 chicken을 선택한 사람 중 코딩테스트 점수를 100점 이상 받은 사람은 모두 몇 명인가?
- 코딩테스트에 cpp로 참여했으며, senior 경력이면서, 소울푸드로 pizza를 선택한 사람 중 코딩테스트 점수를 100점 이상 받은 사람은 모두 몇 명인가?
- backend 직군을 선택했고, senior 경력이면서 코딩테스트 점수를 200점 이상 받은 사람은 모두 몇 명인가?
- 소울푸드로 chicken을 선택한 사람 중 코딩테스트 점수를 250점 이상 받은 사람은 모두 몇 명인가?
- 코딩테스트 점수를 150점 이상 받은 사람은 모두 몇 명인가?

즉, 개발팀에서 궁금해하는 내용은 다음과 같은 형태를 갖습니다.

* [조건]을 만족하는 사람 중 코딩테스트 점수를 X점 이상 받은 사람은 모두 몇 명인가?


## 문제
지원자가 지원서에 입력한 4가지의 정보와 획득한 코딩테스트 점수를 하나의 문자열로 구성한 값의 배열 info, 개발팀이 궁금해하는 문의조건이 문자열 형태로 담긴 배열 query가 매개변수로 주어질 때,
각 문의조건에 해당하는 사람들의 숫자를 순서대로 배열에 담아 return 하도록 solution 함수를 완성해 주세요.


## 제한사항
- info 배열의 크기는 1 이상 50,000 이하입니다.
- info 배열 각 원소의 값은 지원자가 지원서에 입력한 4가지 값과 코딩테스트 점수를 합친 "개발언어 직군 경력 소울푸드 점수" 형식입니다.
   - 개발언어는 cpp, java, python 중 하나입니다.
   - 직군은 backend, frontend 중 하나입니다.
   - 경력은 junior, senior 중 하나입니다.
   - 소울푸드는 chicken, pizza 중 하나입니다.
   - 점수는 코딩테스트 점수를 의미하며, 1 이상 100,000 이하인 자연수입니다.
   - 각 단어는 공백문자(스페이스 바) 하나로 구분되어 있습니다.
- query 배열의 크기는 1 이상 100,000 이하입니다.
- query의 각 문자열은 "[조건] X" 형식입니다.
   - [조건]은 "개발언어 and 직군 and 경력 and 소울푸드" 형식의 문자열입니다.
   - 언어는 cpp, java, python, - 중 하나입니다.
   - 직군은 backend, frontend, - 중 하나입니다.
   - 경력은 junior, senior, - 중 하나입니다.
   - 소울푸드는 chicken, pizza, - 중 하나입니다.
   - '-' 표시는 해당 조건을 고려하지 않겠다는 의미입니다.
   - X는 코딩테스트 점수를 의미하며 조건을 만족하는 사람 중 X점 이상 받은 사람은 모두 몇 명인 지를 의미합니다.
   - 각 단어는 공백문자(스페이스 바) 하나로 구분되어 있습니다.
   - 예를 들면, "cpp and - and senior and pizza 500"은 "cpp로 코딩테스트를 봤으며, 경력은 senior 이면서 소울푸드로 pizza를 선택한 지원자 중 코딩테스트 점수를 500점 이상 받은 사람은 모두 몇 명인가?"를 의미합니다.


## 풀이 방법
1. 하나의 info를 처리할 때, 해당 info가 포함되는 모든 경우에 대해 `map`을 구성한다.
   - ex. java backend junior pizza 150 인 경우
     1) - - - - : 150
     2) - - - p : 150
     3) - - j - : 150
     ...


## 소스코드
```c++
#include <string>
#include <vector>
#include <sstream>  // stringstream
#include <map>  // map
#include <algorithm>    // sort, next_permutation
#include <regex>    // regex

using namespace std;

int getScore(string str){
    stringstream ss(str);
    string lan, job, lev, food, strscore;
    getline(ss, lan, ' '); getline(ss, job, ' ');
    getline(ss, lev, ' '); getline(ss, food, ' ');
    getline(ss, strscore, ' ');
    
    int score = stoi(strscore);
    return score;
}

string getLine(string str){
    stringstream ss(str);
    string lan, job, lev, food, strscore;
    getline(ss, lan, ' '); getline(ss, job, ' ');
    getline(ss, lev, ' '); getline(ss, food, ' ');
    
    string line = "";
    line += lan[0]; line += job[0];
    line += lev[0]; line += food[0];
    return line;
}

vector<int> solution(vector<string> info, vector<string> query) {
    vector<int> answer;
    
    map<string, vector<int>> m;
    for(auto e : info){
        string line = getLine(e);
        int score = getScore(e);
        
        m["----"].push_back(score);
        m[line].push_back(score);
        for(int k = 1; k < 4; k++){
            vector<bool> flags(4, false);
            for(int i = 0; i < k; i++){
                flags[i] = true;
            }
            
            sort(flags.begin(), flags.end());
            do{
                string combo = "";
                for(int i = 0; i < 4; i++){
                    combo += (flags[i] == true) ? line[i] : '-';
                }
                m[combo].push_back(score);
            }while(next_permutation(flags.begin(), flags.end()));
        }
    }
    
    for(auto& e : m){
        sort(e.second.begin(), e.second.end(), [](auto a, auto b){
            return a > b;
        });
    }
    
    for(auto e : query){
        e = regex_replace(e, regex(" and"), "");
        
        string line = getLine(e);
        int score = getScore(e);
        
        auto it = find_if(m[line].begin(), m[line].end(), [score](auto a){
            return a < score;
        });
        int cnt = it - m[line].begin();
        answer.push_back(cnt);
    }
    
    return answer;
}
```