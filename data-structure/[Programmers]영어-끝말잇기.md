
## 문제설명
1부터 n까지 번호가 붙어있는 **n명**의 사람이 영어 끝말잇기를 하고 있습니다. 영어 끝말잇기는 다음과 같은 규칙으로 진행됩니다.

1번부터 번호 순서대로 한 사람씩 차례대로 단어를 말합니다.
마지막 사람이 단어를 말한 다음에는 다시 1번부터 시작합니다.
앞사람이 말한 단어의 마지막 문자로 시작하는 단어를 말해야 합니다.
이전에 등장했던 단어는 사용할 수 없습니다.
한 글자인 단어는 인정되지 않습니다.
다음은 3명이 끝말잇기를 하는 상황을 나타냅니다.

tank → kick → know → wheel → land → dream → mother → robot → tank

위 끝말잇기는 다음과 같이 진행됩니다.

1번 사람이 자신의 첫 번째 차례에 tank를 말합니다.
2번 사람이 자신의 첫 번째 차례에 kick을 말합니다.
3번 사람이 자신의 첫 번째 차례에 know를 말합니다.
1번 사람이 자신의 두 번째 차례에 wheel을 말합니다.
(계속 진행)
끝말잇기를 계속 진행해 나가다 보면, 3번 사람이 자신의 세 번째 차례에 말한 tank 라는 단어는 이전에 등장했던 단어이므로 탈락하게 됩니다.

사람의 수 n과 사람들이 순서대로 말한 단어 words 가 매개변수로 주어질 때, **가장 먼저 탈락하는 사람의 번호**와 그 사람이 **자신의 몇 번째 차례에 탈락하는지**를 구해서 return 하도록 solution 함수를 완성해주세요.


## 제한 사항
- 끝말잇기에 참여하는 사람의 수 n은 2 이상 10 이하의 자연수입니다.
- words는 끝말잇기에 사용한 단어들이 순서대로 들어있는 배열이며, 길이는 n 이상 100 이하입니다.
- 단어의 길이는 **2 이상 50 이하**입니다.
- 모든 단어는 **알파벳 소문자로만** 이루어져 있습니다.
- 끝말잇기에 사용되는 단어의 뜻(의미)은 신경 쓰지 않으셔도 됩니다.
- 정답은 **[ 번호, 차례 ]** 형태로 return 해주세요.
- 만약 주어진 단어들로 탈락자가 생기지 않는다면, [**0, 0**]을 return 해주세요.


## 풀이방법
1) 끝말잇기의 규칙을 만족하는지 체크하기 위해, 바로 이전 단어의 마지막 character와 현재 단어의 첫번째 character가 동일한지 검사한다.  
   (std::string::<span style="background-color:#fff5b1"> front() </span>, 
<span style="background-color:#fff5b1"> 노란형광펜 </span>
3) (, std::string::baack())
4) 이미 말한 단어가 중복되는지 체크하기 위해, 자료구조(set)을 사용한다.
5) 가장 먼저 탈락하는 사람의 번호와 몇 번째 차례에서 탈락하는지를 끝말잇기에 사용한 배열(words)에서의 순서값으로부터 계산한다.
  - 탈락하는 사람의 번호 : (i % n) + 1
  - 탈락한 라운드 : (i / n) + 1


## 소스코드
```C++
#include <string>
#include <vector>
#include <set>  // set

using namespace std;

vector<int> solution(int n, vector<string> words) {
    vector<int> answer(2, 0);
    
    string before = words[0];
    
    set<string> s;
    s.insert(words[0]);
    for(int i = 1; i < words.size(); i++){
        if(before.back() != words[i].front()){
            answer[0] = (i % n) + 1;
            answer[1] = (i / n) + 1;
            break;
        }
        
        auto it = s.find(words[i]);
        if(it != s.end()){
            answer[0] = (i % n) + 1;
            answer[1] = (i / n) + 1;
            break;
        }
        
        before = words[i];
        s.insert(words[i]);
    }

    return answer;
}
```
