# Dijkstra algorithm





``` c++
//
//  케빈 베이컨의 6단계 법칙 (1389) - dijkstra.cpp
//  Algorithm_study
//
//  Created by Yeo Kyu Li on 19/05/2019.
//  Copyright © 2019 Yeo Kyu Li. All rights reserved.
//
/*
5 5
1 3
1 4
4 5
4 3
3 2
*/

#include <iostream>
#include <queue>
#include <vector>
#include <cstring>
using namespace std;
int N, M;
vector <int> v[101];
int dist[101];
int cost[101];

void BFS(int startV){
    priority_queue<int> Q;
    //next, cost
    // 가중치가 있는 경우에는 cost에 -를 넣어 줘야함, 우선순위 큐에 대해서 알아보기!
    Q.push(startV);
    dist[startV] = 0;
    while(!Q.empty()){
        int here = Q.top();
        Q.pop();
        for(int i = 0 ; i < v[here].size(); i++){
            int next = v[here][i];
            // int cost = v[here][i].second;
            // 1 대신에 cost 더해주는걸로!
            if(dist[next] > dist[here] + 1){
                dist[next] = dist[here] + 1;
                Q.push(next);
            }
        }
    }
    for(int i = 1 ; i <= N ; i++){
        cost[startV] += dist[i];
    }
}

int main(){
    
    ios_base::sync_with_stdio();
    cin.tie(0);
    cout.tie(0);
    
    cin >> N >> M;
    int min=1000, minA[101], node=0;
    for(int i = 1 ; i <= M ; i ++){
        int a, b;
        cin >> a >> b;
        //v[a].push_back(make_pair<b,cost>);
        v[a].push_back(b);
        v[b].push_back(a);
    }
    
    for(int i = 1 ; i <= N; i++){
        memset(dist, 10000, sizeof(dist));
        BFS(i);
        if(min > cost[i]){
            min = cost[i];
            node = i;
            minA[i]++;
        }
    }
    
    if(minA[node] == 0)
        cout << min << "\n";
    else
        cout << node << "\n";
    //    cout << *min_element(cost+1, cost+N+1) << endl;
    
}
```

