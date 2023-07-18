## 문제 설명
숫자로 이루어진 문자열 t와 p가 주어질 때, t에서 p와 길이가 같은 부분문자열 중에서, 이 부분문자열이 나타내는
수가 p가 나타내는 수보다 작거나 같은 것이 나오는 횟수를 return하는 함수 solution을 완성하세요.

예를 들어, t="3141592"이고 p="271" 인 경우, t의 길이가 3인 부분 문자열은 314, 141, 415, 159, 592입니다. 이
문자열이 나타내는 수 중 271보다 작거나 같은 수는 141, 159 2개 입니다.


## 제한사항
- 1 ≤ **p의 길이** ≤ **18**
- p의 길이 ≤ **t의 길이** ≤ **10,000**
- t와 p는 숫자로만 이루어진 문자열이며, 0으로 시작하지 않습니다.


## 풀이방법
! This is an info message. 정수 표현범위에 따른 자료형 사용!
> char(1바이트) : 2^8 -> 10진수 2자리까지 완전 커버
> int(4바이트) : 2^32 -> 10진수 9자리까지 완전 커버
> long(windows: 4바이트, 타OS: 8바이트)
> long long(8바이트) : 2^64 -> 10진수 18자리까지 완전 표현


## 
```C++
#include <string>
#include <vector>

using namespace std;

int solution(string t, string p) {
    int answer = 0;
    
    int n = p.size();
    long long value = stoll(p);
    
    for(int i = 0; i <= t.size() - n; i++){
        string sub = t.substr(i, n);
       if(stoll(sub) <= value){
           answer++;
        }
    }
    
    return answer;
}
```
