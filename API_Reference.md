# 중복/반복 원소 제거
## 중복 원소 제거
- Method : `sort()` -> `unique()` -> `erase()` or `자료구조(set)`
 1) **sort(first, last)** : It sorts the elements in the range [first, last) into ascending order. (pre-requisite)
 2) **unique(first, last)** : It removes duplicates of any element present consecutively in a range [first, last).  (RV : the iterator to the element that follows the last element not removed)
 3) **erase(first, last)** or **erase(position)** : It removes from the vector either a range of elements ([first, last)) or a single element (position).

```
# include <algorithm>   // sort, unique

int myints[] = {1, 2, 1, 3, 2, 1, 2};
vector<int> v(myints, myints + sizeof(myints) / sizeof(int));

sort(v.begin(), v.end()); // {1, 1, 1, 2, 2, 2, 3}
auto it = unique(v.begin(), v.end()); // {1, 2, 3, *(2), *(2), *(2), *(3)}
v.erase(it, v.end()); // {1, 2, 3}
```

## 반복 원소 제거
- Method : `unique()` -> `erase()`
 1) **unique()** : 
 2) **erase()** :


-----
# Container (Data Structure)
## string

## vector

## map

```
#include <map>  // map

map<string, int> m;
for(int i = 0; i < participant.size(); i++){
      m[participant[i]] += 1;
}
```

## set


-----
# Algorithm (Library)
## 검색
- `find(first, last, )` : 

find_if

prefix match
string.substr
