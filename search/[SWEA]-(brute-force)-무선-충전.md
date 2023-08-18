## 문제 설명
스마트폰을 무선 충전 할 때 최적의 BC (Battery Charger)를 선택하는 알고리즘을 개발하고자 한다. [그림 1]과 같이 가로 세로 10*10 영역의 지도가 주어졌을 때, 설치된 BC 정보는 다음과 같다.

BC의 충전 범위가 C일 때, BC와 거리가 C 이하이면 BC에 접속할 수 있다. 이때, 두 지점 A(XA, YA), B(XB, YB) 사이의 거리는 다음과 같이 구할 수 있다.

D = |XA – XB| + |YA – YB|

위의 [그림 1]에서 (4,3)과 (5,4) 지점은 BC 1과 BC 3의 충전 범위에 모두 속하기 때문에, 이 위치에서는 두 BC 중 하나를 선택하여 접속할 수 있다.

[그림 2]와 같이 사용자 A와 B의 이동 궤적이 주어졌다고 가정하자. T는 초(Second)를 의미한다. 예를 들어 5초에 사용자 A는 (5, 2) 지점에, 사용자 B는 (6, 9) 지점에 위치한다.

매초마다 특정 BC의 충전 범위에 안에 들어오면 해당 BC에 접속이 가능하다. 따라서 T=5에 사용자 A는 BC 3에, 사용자 B는 BC 2에 접속할 수 있다. 이때, 접속한 BC의 성능(P)만큼 배터리를 충전 할 수 있다. 만약 한 BC에 두 명의 사용자가 접속한 경우, 접속한 사용자의 수만큼 충전 양을 균등하게 분배한다.

BC의 정보와 사용자의 이동 궤적이 주어졌을 때, 모든 사용자가 충전한 양의 합의 최댓값을 구하는 프로그램을 작성하라.

[그림 2]에서 T=11일 때, 사용자 A는 BC 1과 3 둘 중 하나에 접속이 가능하다. 같은 시간에 사용자 B는 BC 1에 접속할 수 밖에 없다. 따라서 사용자 A가 같은 BC 1에 접속한다면 충전되는 양를 반씩 나눠 갖게 되어 비효율적이다. 따라서 사용자 A가 BC 3에 접속하는 것이 더 이득이다.

위 예제에서 매 초마다 충전한 양은 다음과 같다. 따라서 총 충전한 양의 총합은 720 + 480 = 1200 이다.


## 제한사항
1. 지도의 가로, 세로 크기는 10이다.
2. 사용자는 총 2명이며, 사용자A는 지도의 (1, 1) 지점에서, 사용자B는 지도의 (10, 10) 지점에서 출발한다.
3. 총 이동 시간 M은 20이상 100이하의 정수이다. (20 ≤ M ≤ 100)
4. BC의 개수 A는 1이상 8이하의 정수이다. (1 ≤ A ≤ 8)
5. BC의 충전 범위 C는 1이상 4이하의 정수이다. (1 ≤ C ≤ 4)
6. BC의 성능 P는 10이상 500이하의 짝수이다. (10 ≤ P ≤ 500)
7. 사용자의 초기 위치(0초)부터 충전을 할 수 있다.
8. 같은 위치에 2개 이상의 BC가 설치된 경우는 없다. 그러나 사용자A, B가 동시에 같은 위치로 이동할 수는 있다. 사용자가 지도 밖으로 이동하는 경우는 없다.


## 풀이 방법
1. 매 T초마다, 사용자 A와 B의 이동한 좌표가 BC와의 충전 범위 내에 포함되는지 확인한다.
  - 충전 범위 내에 포함된 경우, 각 사용자 별 충전 가능한 BC에 포함한다.

2. 모든 이동 궤적을 지난 후, 매 초마다 충전 가능한 BC의 조합 중 최댓값을 계산한다.


## 소스코드
```c++
#include <vector>
#include <iostream>

using namespace std;

int getTotal(vector<int> aap, vector<int> bap, vector<vector<int>> aps){
    int total = 0;
    if(aap.size() == 0 && bap.size() == 0){
        return 0;
    }

    if(aap.size() == 0 || bap.size() == 0){
        auto targetap = (aap.size() == 0) ? bap : aap;
        for(auto a : targetap){
            total = max(total, aps[a][3]);
        }

        return total;
    }

    auto baseap = (aap.size() >= bap.size()) ? aap : bap;
    auto compareap = (aap.size() >= bap.size()) ? bap : aap;
    for(auto a : baseap){
        for(auto b : compareap){
            int sum = aps[a][3];
            if(a != b){
                sum += aps[b][3];
            }
            total = max(total, sum);
        }
    }
    return total;
}

vector<int> getRangedAps(int ay, int ax, vector<vector<int>> aps){
    vector<int> rangedAps;
    for(int i = 0; i < aps.size(); i++){
        auto ap = aps[i];
        int x = ap[0] - 1, y = ap[1] - 1, c = ap[2], p = ap[3];

        if(abs(ay - y) + abs(ax - x) <= c){
            rangedAps.push_back(i);
        }
    }
    return rangedAps;
}

int dy[] = {0, -1, 0, 1, 0};
int dx[] = {0, 0, 1, 0, -1};

int solution(int M, int A, vector<int> auser, vector<int> buser, vector<vector<int>> aps){
    int answer = 0;

    int ay = 0, ax = 0;
    int by = 9, bx = 9;
    answer += getTotal(getRangedAps(ay, ax, aps), getRangedAps(by, bx, aps), aps);
    
    for(int t = 0; t < auser.size(); t++){
        // 위치 이동
        ay = ay + dy[auser[t]]; ax = ax + dx[auser[t]];
        by = by + dy[buser[t]]; bx = bx + dx[buser[t]];
        
        vector<int> aap = getRangedAps(ay, ax, aps);
        vector<int> bap = getRangedAps(by, bx, aps);
        
        int total = getTotal(aap, bap, aps);
        answer += total;
    }

    return answer;
}

int main(int argc, char** argv)
{
	int test_case;
	int T;

    //freopen("Input.txt", "r", stdin);
	cin>>T;
    
	/*
	   여러 개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
	*/
	for(test_case = 1; test_case <= T; ++test_case)
	{
        int M = 0, A = 0;
        cin >> M >> A;
        
        int move = 0;
        vector<int> auser, buser;
        for(int i = 0; i < M; i++){
            cin >> move;
            auser.push_back(move);
        }
        for(int i = 0; i < M; i++){
            cin >> move;
            buser.push_back(move);
        }

        vector<vector<int>> aps;
        int X = 0, Y = 0, C = 0, P = 0;
        for(int i = 0; i < A; i++){
            cin >> X >> Y >> C >> P;
            vector<int> ap;
            ap.push_back(X);
            ap.push_back(Y);
            ap.push_back(C);
            ap.push_back(P);
            aps.push_back(ap);
        }
        
        cout << "#" << test_case << " " << solution(M, A, auser, buser, aps) << endl;
	}
    
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```