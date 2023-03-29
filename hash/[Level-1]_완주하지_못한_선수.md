# 완주하지 못한 선수
![image](https://user-images.githubusercontent.com/97339878/228542439-b45d42d0-80c7-4ba7-a4b5-76152558b67d.png)
![image](https://user-images.githubusercontent.com/97339878/228542516-de285cfc-56ca-4ed6-84c9-bc73890d3ba7.png)


## Solution
```
#include <string>
#include <vector>
#include <map>  // map
#include <algorithm>    // find_if

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    
    map<string, int> mymap;
    for(int i = 0; i < participant.size(); i++){
        mymap[participant[i]] += 1;
    }
    
    for(int i = 0; i < completion.size(); i++){
        mymap[completion[i]] -= 1;
    }
    
    auto it = find_if(mymap.begin(), mymap.end(), [](auto a){
        return (a.second != 0) ? true : false;
    });
    
    answer = it->first;
    return answer;
}
```
