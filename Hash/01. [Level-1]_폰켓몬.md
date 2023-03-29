# 폰켓몬

![image](https://user-images.githubusercontent.com/97339878/228541175-54e8d7a7-de9b-43f9-bdc4-281e11f3c675.png)
![image](https://user-images.githubusercontent.com/97339878/228541411-b3a33df7-bd8e-416d-a228-1b723f14218a.png)
![image](https://user-images.githubusercontent.com/97339878/228541581-127a58c3-b3f5-4d1a-bb57-c4f04ce30b5e.png)

# Solution
```
#include <vector>
#include <algorithm>    // sort

using namespace std;

int solution(vector<int> nums){
    int answer = nums.size()/2;
    
    sort(nums.begin(), nums.end());
    auto it = unique(nums.begin(), nums.end());
    nums.erase(it, nums.end());
    
    if(nums.size() < answer){
        answer = nums.size();
    }
    
    return answer;
}
```
