# 같은 숫자는 싫어

![image](https://user-images.githubusercontent.com/97339878/228838431-aea7746f-26b5-4d7c-86f2-0b98891feeb5.png)
![image](https://user-images.githubusercontent.com/97339878/228838526-b6487e3a-19cb-4d1c-a3db-da45a21d4166.png)

## Solution
```
#include <vector>
#include <algorithm>    // unique

using namespace std;

vector<int> solution(vector<int> arr) {
    vector<int> answer = arr;
    
    auto it = unique(answer.begin(), answer.end());
    answer.erase(it, answer.end());
    
    return answer;
}
```
