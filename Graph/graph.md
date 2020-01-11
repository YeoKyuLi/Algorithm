# Graph

####What is Graph?

​		A Graph is **non-linear** data structure consisting of nodes and edges.

​		The only catch here is, unlike tress, graphs may contain cycles.

![](https://www.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)



###Representations

Following two are the most commonly used representations of a graph.

1. Adjacency Matrix

   Adjacency Matrix is a 2D array of size V x V where V is the number of vertices in a graph.

   If adj\[i][j] = w, then there is an edge from vertex i to vertex j with weight w.

   ![](https://media.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

   ​		**Pros :**

      - Representation is easier to implement and follow.

      - Removing an edge takes O(1) time. Queries like whether there is an edge from vertex 'u' to vertex 'v' are efficient and can be done O(1).

        

        **Cons : **

   - Consumes more space O(V^2). Even if the graph is sparse, it consumes the same space.

   

   

2. Adjacency List : weighted graph

   An array of lists is used. Size of the array is equal to the number of vertices. **array[]**. An entry array[i] represents the list of vertices adjacent to the *i* th vertex.

![Adjacency List Representation of Graph](https://media.geeksforgeeks.org/wp-content/uploads/listadjacency.png)



### Breadth First Search or BFS for a Graph

Breath First Traversal (or Search) for a graph is similar to Breadth First Traversal of a tree.

To avoid processing a node more than once, using a boolean visited array.

It's using Queue and Visitied[] to representation of BFS.

Time Complexity : O(V+E)

2 - 0 - 3 - 1

![img](https://media.geeksforgeeks.org/wp-content/uploads/bfs-5.png)





### Depth First Search or DFS for a Graph

Depth First Traversal (or Search) for a graph is similar to Depth First Traveral of a tree.

Time Complexity : O(V+E)

2 - 0 - 1 - 3

![img](https://media.geeksforgeeks.org/wp-content/uploads/cycle.png)



DFS and BFS

[site](https://www.acmicpc.net/problem/1260)

```c++
/*
#### Adjacency List ####   ******************************************************************************
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





<<Graph representations using set and hash(unordered_set)>>



* **Frequently Problems**

  - [Height of a generic tree from parent array](https://www.geeksforgeeks.org/height-generic-tree-parent-array/)
  - [DFS for a n-ary tree (acyclic graph) represented as adjacency list](https://www.geeksforgeeks.org/dfs-n-ary-tree-acyclic-graph-represented-adjacency-list/)
  - [BFS for Disconnected Graph](https://www.geeksforgeeks.org/bfs-disconnected-graph/)
  - 

  

* Graph Cycle
  * [Detect Cycle in a Directed Graph](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)
  * [Detect cycle in an undirected graph](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)
  * [Detect cycle in a direct graph using colors](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)
  * [Detect a negative cycle in a Graph | (Bellman Ford)](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/)
  * 



* Topological Sorting
  * [Topological Sorting](https://www.geeksforgeeks.org/topological-sorting/)
  * [Kahn’s Algorithm for Topological Sorting](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)
  * [Longest Path in a Directed Acyclic Graph](https://www.geeksforgeeks.org/find-longest-path-directed-acyclic-graph/)
  * 

* Minimum Spanning Tree
  * [Prim’s Minimum Spanning Tree (MST))](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)
  * [Minimum Product Spanning Tree](https://www.geeksforgeeks.org/minimum-product-spanning-tree/)
  * 
* BackTracking
  * [n-Queen’s Problem](https://www.geeksforgeeks.org/backtracking-set-3-n-queen-problem/)
  * [m Coloring Problem](https://www.geeksforgeeks.org/backttracking-set-5-m-coloring-problem/)
  * [Permutation of numbers such that sum of two consecutive numbers is a perfect square](https://www.geeksforgeeks.org/permutation-numbers-sum-two-consecutive-numbers-perfect-square/)
  * 
* **Shortest Paths**
  * [Dijkstra’s shortest path algorithm](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)
  * [Dijkstra’s Algorithm for Adjacency List Representation](https://www.geeksforgeeks.org/greedy-algorithms-set-7-dijkstras-algorithm-for-adjacency-list-representation/)
  * [Bellman–Ford Algorithm](https://www.geeksforgeeks.org/dynamic-programming-set-23-bellman-ford-algorithm/)
  * [Floyd Warshall Algorithm](https://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/)
* LeetCode
  * [Graph](https://leetcode.com/tag/graph/)
  * [Depth-first Search](https://leetcode.com/tag/depth-first-search/)
  * [Breadth-first Search](https://leetcode.com/tag/breadth-first-search/)
  * 
* s







