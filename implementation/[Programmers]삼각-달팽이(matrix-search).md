## 문제 설명
정수 n이 매개변수로 주어집니다. 다음 그림과 같이 밑변의 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 return 하도록 solution 함수를 완성해주세요.


## 제한사항
- n은 1 이상 1,000 이하입니다.


## 풀이 방법
1. 문제 설명에 따라 제한사항(밑변의 길이와 높이 = n) 내에서 맨 위 꼭짓점부터 `반시계 방향`으로 숫자를 채운다.
   - 아래방향 : 시작점부터 이동범위(down)까지 y++
   - 오른쪽방향 : 시작점부터 이동범위(right)까지 x++
   - 대각선위쪽방향 : 시작점부터 이동범위(up & left)까지 y-- && x--

2. `시작위치`는 다음 방향으로 진행시 올바른 시작위치로 조정한다.
  - 아래방향 종료 후 : y-- & x++
  - 오른쪽방향 종료 후 : y-- && x -= 2
  - 대각선위쪽방향 종료 후 : y += 2 && x++

3. `이동범위`는 이동 가능한 범위로 재조정한다.
  - 아래방향 종료 후 : down--
  - 오른쪽방향 종료 후 : right -= 2
  - 대각선위쪽방향 종료 후 : up -= 2 && left--


## 소스코드
```c++
#include <string>
#include <vector>

using namespace std;

int matrix[1001][1001];

vector<int> solution(int n) {
    vector<int> answer;
    
    int limit = 0;
    for(int i = n; i > 0; i--){
        limit += i;
    }
    
    int num = 1;
    int flag = 0;   // 0 (down), 1(right), 2(cross-up)
    int up = 0, left = 0, down = n, right = n;
    int cy = 0, cx = 0;
    while(num <= limit){
        if(flag == 0){
            while(cy < down){
                matrix[cy++][cx] = num++;
            }
            cy--; cx++;
            down--;
            flag = 1;
        }else if(flag == 1){
            while(cx < right){
                matrix[cy][cx++] = num++;
            }
            cx -= 2; cy--;
            right -= 2;
            flag = 2;
        }else if(flag == 2){
            while(cy > up && cx > left){
                matrix[cy--][cx--] = num++;
            }
            cy += 2; cx++;
            up += 2; left++;
            flag = 0;
        }
    }
    
    for(int y = 0; y < n; y++){
        for(int x = 0; x < y+1; x++){
            answer.push_back(matrix[y][x]);
        }
    }
    
    return answer;
}
```