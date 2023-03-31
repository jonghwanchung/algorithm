
-----
# Container (Data Structure)
## string
string.substr

## vector

## map
- It stores the elements formed by a combination of a `key` and a mapped `value` (key-value pair), following a specific order.

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
```
```

- `find_if(first, last, unary)` : It returns an iterator to the first element in the range [first,last) for which pred returns true.  (If no such element is found, the function returns last/end.
```
int myints[] = {1, 2, 3, 4};
vector<int> v(myints, myints + sizeof(myints) / sizeof(int));

auto it = find_if(v.begin(), v.end(), [](auto a){
        return (a % 2 == 0) ? true : false;
});
if(it != v.end()){
        cout << *it << endl;  // 2
}
```


