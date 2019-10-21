# Graph



DFS and BFS

```c++
/******************************************************************************
//  DFS and BFS (1260).cpp
4 5 1
1 2
1 3
1 4
2 4
3 4
DFS -> BFS
1 2 4 3
1 2 3 4

5 5 3
5 4
5 2
1 2
3 4
3 1
DFS -> BFS
3 1 2 5 4
3 1 4 2 5

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 
다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 
어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.
*******************************************************************************/
#include <iostream>
#include <algorithm>
#include <queue>
#include <cstring>
using namespace std;

const int MAX = 1001;
bool visited[MAX];
vector<int> adj[MAX];
queue<int> Q;

void DFS(int x)
{
    visited[x] = true;
    cout << x << " ";
    for(int y : adj[x])
    {
        if(!visited[y])
            DFS(y);
    }
}

void BFS(int x)
{
    Q.push(x);
    visited[x] = true;
    while(!Q.empty())
    {
        int value = Q.front();
        Q.pop();
        cout << value << " " ;
        for(int y : adj[value])
        {
            if(!visited[y])
            {
                Q.push(y);
                visited[y] = true;
            }
        }
        
    }
}

int main()
{
    int n, m, v;
    
    cin >> n >> m >> v;
    
    for(int i = 0 ; i < m; i++)
    {
        int r, l;
        cin >> r >> l;
        adj[r].push_back(l);
        adj[l].push_back(r);
    }
    for(int i = 1 ; i <=n ; i++){
        sort(adj[i].begin(), adj[i].end());
    }
    
    // cout << endl;
    // for(int i = 1 ; i <= n ; i++){
    //     cout << i << " ";
    //     for(int x : adj[i])
    //         cout << x << " ";
    //     cout << endl;
    // }
    
    DFS(v);
    memset(visited, 0, sizeof(visited));
    cout << endl;
    BFS(v);
    return 0;
}
```

