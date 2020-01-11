# BFS

1. Number of Islands - Medium

   Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

   **Example 1:**

   ```
   Input:
   11110
   11010
   11000
   00000
   
   Output: 1
   ```

   **Example 2:**

   ```
   Input:
   11000
   11000
   00100
   00011
   
   Output: 3
   ```

   ```c++
   class Solution {
   private:
       int result;
   
       bool visited[101][101];
       void BFS(int r, int c, vector<vector<char>>& grid, int V, int H)
       {
           int dx[] = {-1, 0, 1, 0};
           int dy[] = {0, 1, 0, -1};
           
           queue<pair<int,int>> q;
           grid[r][c] = '0';
           q.push(make_pair(r,c));
           
           while(!q.empty())
           {
               int x = q.front().first;
               int y = q.front().second;
               q.pop();
               
               for(int i = 0 ; i < 4; i++)
               {
                   int nx = x + dx[i];
                   int ny = y + dy[i];
                   if(nx >= 0 && ny>=0 && nx < V && ny < H)
                   {
                       if(grid[nx][ny] == '1')
                       {
                           grid[nx][ny] = '0';
                           q.push(make_pair(nx,ny));
                       }
                   }
                   
               }
           }
       }
       
   public:
       int numIslands(vector<vector<char>>& grid) {
           int result = 0;
           
           for(int i = 0 ; i < grid.size(); i++)
           {
               for(int j = 0 ; j < grid[0].size(); j++)
               {
                   if(grid[i][j] == '1')
                   {
                       BFS(i,j, grid, grid.size(), grid[0].size());
                       result++;
                   }
               }
           }
           
           return result;        
       }
   };
   ```

   

2. **Convert Sorted Array to Binary Search Tree** - Easy

   [site](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

   Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

   For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

   **Example:**

   ```
   Given the sorted array: [-10,-3,0,5,9],
   
   One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
   
         0
        / \
      -3   9
      /   /
    -10  5
   ```

   ```c++
   /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   #include <algorithm>
   class Solution {
   public:
       TreeNode* createdBST(vector<int>& nums, int start, int end){
           if(start > end)
               return NULL;
           
           int mid = (start + end)/2;
           TreeNode* node = new TreeNode(nums[mid]);
           
           node->left = createdBST(nums, start, mid-1);
           node->right = createdBST(nums, mid+1, end);
   
           return node;
           
       }
       TreeNode* sortedArrayToBST(vector<int>& nums) {
           
           return createdBST(nums, 0, nums.size()-1);
       }
   };
   ```

3. 유기농 배추 성공 1012

   [site](https://www.acmicpc.net/problem/1012)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 1 초      | 512 MB      | 41611 | 14560 | 9990      | 33.983%   |

   ## 문제

   차세대 영농인 한나는 강원도 고랭지에서 유기농 배추를 재배하기로 하였다. 농약을 쓰지 않고 배추를 재배하려면 배추를 해충으로부터 보호하는 것이 중요하기 때문에, 한나는 해충 방지에 효과적인 배추흰지렁이를 구입하기로 결심한다. 이 지렁이는 배추근처에 서식하며 해충을 잡아 먹음으로써 배추를 보호한다. 특히, 어떤 배추에 배추흰지렁이가 한 마리라도 살고 있으면 이 지렁이는 인접한 다른 배추로 이동할 수 있어, 그 배추들 역시 해충으로부터 보호받을 수 있다.

   (한 배추의 상하좌우 네 방향에 다른 배추가 위치한 경우에 서로 인접해있다고 간주한다)

   한나가 배추를 재배하는 땅은 고르지 못해서 배추를 군데군데 심어놓았다. 배추들이 모여있는 곳에는 배추흰지렁이가 한 마리만 있으면 되므로 서로 인접해있는 배추들이 몇 군데에 퍼져있는지 조사하면 총 몇 마리의 지렁이가 필요한지 알 수 있다.

   예를 들어 배추밭이 아래와 같이 구성되어 있으면 최소 5마리의 배추흰지렁이가 필요하다.

   (0은 배추가 심어져 있지 않은 땅이고, 1은 배추가 심어져 있는 땅을 나타낸다.)

   | **1** | **1** | 0     | 0     | 0     | 0    | 0    | 0     | 0     | 0     |
   | ----- | ----- | ----- | ----- | ----- | ---- | ---- | ----- | ----- | ----- |
   | 0     | **1** | 0     | 0     | 0     | 0    | 0    | 0     | 0     | 0     |
   | 0     | 0     | 0     | 0     | **1** | 0    | 0    | 0     | 0     | 0     |
   | 0     | 0     | 0     | 0     | **1** | 0    | 0    | 0     | 0     | 0     |
   | 0     | 0     | **1** | **1** | 0     | 0    | 0    | **1** | **1** | **1** |
   | 0     | 0     | 0     | 0     | **1** | 0    | 0    | **1** | **1** | **1** |

   ## 입력

   입력의 첫 줄에는 테스트 케이스의 개수 T가 주어진다. 그 다음 줄부터 각각의 테스트 케이스에 대해 첫째 줄에는 배추를 심은 배추밭의 가로길이 M(1 ≤ M ≤ 50)과 세로길이 N(1 ≤ N ≤ 50), 그리고 배추가 심어져 있는 위치의 개수 K(1 ≤ K ≤ 2500)이 주어진다. 그 다음 K줄에는 배추의 위치 X(0 ≤ X ≤ M-1), Y(0 ≤ Y ≤ N-1)가 주어진다.

   ## 출력

   각 테스트 케이스에 대해 필요한 최소의 배추흰지렁이 마리 수를 출력한다.

   ## 예제 입력 1 복사

   ```
   2
   10 8 17
   0 0
   1 0
   1 1
   4 2
   4 3
   4 5
   2 4
   3 4
   7 4
   8 4
   9 4
   7 5
   8 5
   9 5
   7 6
   8 6
   9 6
   10 10 1
   5 5
   ```

   ## 예제 출력 1 복사

   ```
   5
   1
   ```

   ```c++
   //
   //  유기농 배추 (1012).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 02/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   // 인접리스트로 풀기!!
   #include <iostream>
   #include <queue>
   #include <cstring> // memset
   using namespace std;
   int V, H;
   int arr[101][101];
   bool visited[101][101];
   int dx[] = {0, 0, 1, -1};
   int dy[] = {1, -1, 0, 0};
   void input()
   {
       int N;
       cin >> V >> H >> N;
       while(N--){
           int a,b;
           cin >> a >> b;
           arr[a][b] = 1;
       }
       
       
   }
   
   void BFS(int a , int b){
       queue<pair<int, int>> Q;
       Q.push(make_pair(a, b));
       visited[a][b] = true;
       
       while(!Q.empty()){
           int x = Q.front().first;
           int y = Q.front().second;
           Q.pop();
           
           for(int i = 0 ; i < 4; i++){
               int nx = x + dx[i];
               int ny = y + dy[i];
               if(nx >= 0 && ny >= 0 && nx < V && ny < H ){
                   if(!visited[nx][ny]){
                       if(arr[nx][ny] == 1){
                           visited[nx][ny] = true;
                           Q.push(make_pair(nx, ny));
                       }
                   }
               }
           }
           
       }
   }
   int main()
   {
       ios_base::sync_with_stdio();
       cin.tie(0);
       cout.tie(0);
       int T;
       cin >> T;
       
       while(T--){
           int earthworm=0;
           input();
           for(int i = 0 ; i < V ; i ++){
               for(int j = 0 ; j < H; j++){
                   if(!visited[i][j] && arr[i][j]){
                       BFS(i,j);
                       earthworm++;
                   }
               }
           }
           memset(arr, 0, sizeof(arr));
           memset(visited, false, sizeof(visited));
           cout <<earthworm << endl;
       }
       
       
       return 0;
   }
   
   ```

4. 요세푸스 문제 성공 - 1158

   [site](https://www.acmicpc.net/problem/1158)

   | 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :---- | :-------- | :-------- |
   | 2 초      | 256 MB      | 24369 | 11882 | 8713      | 49.851%   |

   ## 문제

   요세푸스 문제는 다음과 같다.

   1번부터 N번까지 N명의 사람이 원을 이루면서 앉아있고, 양의 정수 K(≤ N)가 주어진다. 이제 순서대로 K번째 사람을 제거한다. 한 사람이 제거되면 남은 사람들로 이루어진 원을 따라 이 과정을 계속해 나간다. 이 과정은 N명의 사람이 모두 제거될 때까지 계속된다. 원에서 사람들이 제거되는 순서를 (N, K)-요세푸스 순열이라고 한다. 예를 들어 (7, 3)-요세푸스 순열은 <3, 6, 2, 7, 5, 1, 4>이다.

   N과 K가 주어지면 (N, K)-요세푸스 순열을 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 N과 K가 빈 칸을 사이에 두고 순서대로 주어진다. (1 ≤ K ≤ N ≤ 5,000)

   ## 출력

   예제와 같이 요세푸스 순열을 출력한다.

   ## 예제 입력 1 복사

   ```
   7 3
   ```

   ## 예제 출력 1 복사

   ```
   <3, 6, 2, 7, 5, 1, 4>
   ```

   ```c++
   //
   //  조세퍼스(1158).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 27/03/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <queue>
   using namespace std;
   
   int main()
   {
       int N, M;
       queue<int> que;
       
       cin >> N >> M;
       
       for(int i = 1 ; i <= N; i++){
           que.push(i);
       }
       cout << "<" ;
       while(!que.empty()){
           if(que.size() == 1){
               cout << que.front() << ">" << endl;
               que.pop();
               break;
           }
           for(int j = 1 ; j < M ; j++){
               que.push(que.front());
               que.pop();
           }
           cout << que.front() <<", ";
           que.pop();
       }
       return 0;
   }
   ```

5. 1389 케빈 베이컨의 6단계 법칙

   [site](https://www.acmicpc.net/problem/1389)

   | 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :--- | :--- | :-------- | :-------- |
   | 2 초      | 128 MB      | 9214 | 4816 | 3775      | 54.021%   |

   ## 문제

   케빈 베이컨의 6단계 법칙에 의하면 지구에 있는 모든 사람들은 최대 6단계 이내에서 서로 아는 사람으로 연결될 수 있다. 케빈 베이컨 게임은 임의의 두 사람이 최소 몇 단계 만에 이어질 수 있는지 계산하는 게임이다.

   예를 들면, 전혀 상관없을 것 같은 인하대학교의 이강호와 서강대학교의 민세희는 몇 단계만에 이어질 수 있을까?

   천민호는 이강호와 같은 학교에 다니는 사이이다. 천민호와 최백준은 Baekjoon Online Judge를 통해 알게 되었다. 최백준과 김선영은 같이 Startlink를 창업했다. 김선영과 김도현은 같은 학교 동아리 소속이다. 김도현과 민세희는 같은 학교에 다니는 사이로 서로 알고 있다. 즉, 이강호-천민호-최백준-김선영-김도현-민세희 와 같이 5단계만 거치면 된다.

   케빈 베이컨은 미국 헐리우드 영화배우들 끼리 케빈 베이컨 게임을 했을때 나오는 단계의 총 합이 가장 적은 사람이라고 한다.

   오늘은 Baekjoon Online Judge의 유저 중에서 케빈 베이컨의 수가 가장 작은 사람을 찾으려고 한다. 케빈 베이컨 수는 모든 사람과 케빈 베이컨 게임을 했을 때, 나오는 단계의 합이다.

   예를 들어, BOJ의 유저가 5명이고, 1과 3, 1과 4, 2와 3, 3과 4, 4와 5가 친구인 경우를 생각해보자.

   1은 2까지 3을 통해 2단계 만에, 3까지 1단계, 4까지 1단계, 5까지 4를 통해서 2단계 만에 알 수 있다. 따라서, 케빈 베이컨의 수는 2+1+1+2 = 6이다.

   2는 1까지 3을 통해서 2단계 만에, 3까지 1단계 만에, 4까지 3을 통해서 2단계 만에, 5까지 3과 4를 통해서 3단계 만에 알 수 있다. 따라서, 케빈 베이컨의 수는 2+1+2+3 = 8이다.

   3은 1까지 1단계, 2까지 1단계, 4까지 1단계, 5까지 4를 통해 2단계 만에 알 수 있다. 따라서, 케빈 베이컨의 수는 1+1+1+2 = 5이다.

   4는 1까지 1단계, 2까지 3을 통해 2단계, 3까지 1단계, 5까지 1단계 만에 알 수 있다. 4의 케빈 베이컨의 수는 1+2+1+1 = 5가 된다.

   마지막으로 5는 1까지 4를 통해 2단계, 2까지 4와 3을 통해 3단계, 3까지 4를 통해 2단계, 4까지 1단계 만에 알 수 있다. 5의 케빈 베이컨의 수는 2+3+2+1 = 8이다.

   5명의 유저 중에서 케빈 베이컨의 수가 가장 작은 사람은 3과 4이다.

   BOJ 유저의 수와 친구 관계가 입력으로 주어졌을 때, 케빈 베이컨의 수가 가장 작은 사람을 구하는 프로그램을 작성하시오.

    

   ## 입력

   첫째 줄에 유저의 수 N (2 ≤ N ≤ 100)과 친구 관계의 수 M (1 ≤ M ≤ 5,000)이 주어진다. 둘째 줄부터 M개의 줄에는 친구 관계가 주어진다. 친구 관계는 A와 B로 이루어져 있으며, A와 B가 친구라는 뜻이다. A와 B가 친구이면, B와 A도 친구이며, A와 B가 같은 경우는 없다. 친구 관계는 중복되어 들어올 수도 있으며, 친구가 한 명도 없는 사람은 없다. 또, 모든 사람은 친구 관계로 연결되어져 있다.

   ## 출력

   첫째 줄에 BOJ의 유저 중에서 케빈 베이컨의 수가 가장 작은 사람을 출력한다. 그런 사람이 여러 명일 경우에는 번호가 가장 작은 사람을 출력한다.

   ## 예제 입력 1 복사

   ```
   5 5
   1 3
   1 4
   4 5
   4 3
   3 2
   ```

   ## 예제 출력 1 복사

   ```
   3
   ```

   ```c++
   //
   //  케빈 베이컨의 6단계 법칙 (1389) - 인접행렬.cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 16/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
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

6. 10026 적록색약

   [site](https://www.acmicpc.net/problem/10026)

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 1 초      | 128 MB      | 10163 | 5772 | 4618      | 57.833%   |

   ## 문제

   적록색약은 빨간색과 초록색의 차이를 거의 느끼지 못한다. 따라서, 적록색약인 사람이 보는 그림은 아닌 사람이 보는 그림과는 좀 다를 수 있다.

   크기가 N×N인 그리드의 각 칸에 R(빨강), G(초록), B(파랑) 중 하나를 색칠한 그림이 있다. 그림은 몇 개의 구역으로 나뉘어져 있는데, 구역은 같은 색으로 이루어져 있다. 또, 같은 색상이 상하좌우로 인접해 있는 경우에 두 글자는 같은 구역에 속한다. (색상의 차이를 거의 느끼지 못하는 경우도 같은 색상이라 한다)

   예를 들어, 그림이 아래와 같은 경우에

   ```
   RRRBB
   GGBBB
   BBBRR
   BBRRR
   RRRRR
   ```

   적록색약이 아닌 사람이 봤을 때 구역의 수는 총 4개이다. (빨강 2, 파랑 1, 초록 1) 하지만, 적록색약인 사람은 구역을 3개 볼 수 있다. (빨강-초록 2, 파랑 1)

   그림이 입력으로 주어졌을 때, 적록색약인 사람이 봤을 때와 아닌 사람이 봤을 때 구역의 수를 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 N이 주어진다. (1 ≤ N ≤ 100)

   둘째 줄부터 N개 줄에는 그림이 주어진다.

   ## 출력

   적록색약이 아닌 사람이 봤을 때의 구역의 개수와 적록색약인 사람이 봤을 때의 구역의 수를 공백으로 구분해 출력한다.

   ## 예제 입력 1 복사

   ```
   5
   RRRBB
   GGBBB
   BBBRR
   BBRRR
   RRRRR
   ```

   ## 예제 출력 1 복사

   ```
   4 3
   ```

   ```c++
   //
   //  적록색약 (10026).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 02/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <queue>
   #include <cstring>
   
   using namespace std;
   int N;
   char arr[101][101];
   bool visited[101][101];
   
   //상, 왼, 하, 오
   int dx[] = {0, 0, 1, -1};
   int dy[] = {-1, 1, 0, 0};
   
   void Input(){
       cin >> N;
       
       for(int i = 0 ; i < N; i++){
           for(int j = 0 ; j <N ; j++){
               cin >> arr[i][j];
           }
       }
   }
   void BFS(int a, int b){
       queue<pair<int, int>> Q;
       Q.push(make_pair(a,b));
       visited[a][b] = true;
       
       while(!Q.empty()){
           int x = Q.front().first;
           int y = Q.front().second;
           Q.pop();
           
           for(int i = 0 ; i < 4; i++){
               int nx = x + dx[i];
               int ny = y + dy[i];
               
               if(nx >= 0 && ny >= 0 && nx < N && ny < N){
                   if(!visited[nx][ny]){
                       if(arr[nx][ny] == arr[x][y]){
                           visited[nx][ny] = true;
                           Q.push(make_pair(nx,ny));
                       }
                   }
               }
           }
           
       }
       
   }
   int main()
   {
       Input();
       
       ios_base::sync_with_stdio();
       cin.tie(0);
       cout.tie(0);
       int normal, colorWeak;
       normal = colorWeak = 0;
       
       for(int i = 0 ; i < N ; i++){
           for(int j = 0 ; j < N; j++){
               if(!visited[i][j]){
                   BFS(i,j);
                   normal++;
               }
           }
       }
       
       memset(visited, false, sizeof(visited));
       
       for(int i = 0 ; i < N ; i++){
           for(int j = 0 ; j < N; j++){
               if(arr[i][j] == 'G')
                   arr[i][j] = 'R';
           }
       }
   
       for(int i = 0 ; i < N ; i++){
           for(int j = 0 ; j < N; j++){
               if(!visited[i][j]){
                   BFS(i,j);
                   colorWeak++;
               }
           }
       }
       
       cout << normal << " " << colorWeak << endl;
       
       return 0;
   }
   
   ```

7. 11725 - 트리의 부모 찾기

   [site](https://www.acmicpc.net/submit/11725/12843956)

   | 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :--- | :--- | :-------- | :-------- |
   | 1 초      | 256 MB      | 9372 | 3913 | 2900      | 43.511%   |

   ## 문제

   루트 없는 트리가 주어진다. 이때, 트리의 루트를 1이라고 정했을 때, 각 노드의 부모를 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 노드의 개수 N (2 ≤ N ≤ 100,000)이 주어진다. 둘째 줄부터 N-1개의 줄에 트리 상에서 연결된 두 정점이 주어진다.

   ## 출력

   첫째 줄부터 N-1개의 줄에 각 노드의 부모 노드 번호를 2번 노드부터 순서대로 출력한다.

   ## 예제 입력 1 복사

   ```
   7
   1 6
   6 3
   3 5
   4 1
   2 4
   4 7
   ```

   ## 예제 출력 1 복사

   ```
   4
   6
   1
   3
   1
   4
   ```

   ## 예제 입력 2 복사

   ```
   12
   1 2
   1 3
   2 4
   3 5
   3 6
   4 7
   4 8
   5 9
   5 10
   6 11
   6 12
   ```

   ## 예제 출력 2 복사

   ```
   1
   1
   2
   3
   3
   4
   4
   5
   5
   6
   6
   ```

   

   ```c++
   //
   //  트리의 부모 찾기 (11725).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 18/04/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <vector>
   #include <queue>
   using namespace std;
   
   const int MAX = 100001;
   
   vector<vector<int>> tree(MAX);
   int parents[MAX];
   bool visited[MAX];
   
   int main()
   {
       
       int cnt;
       
       cin >> cnt;
       
       for(int i = 0 ; i < cnt-1; i++){
           int a,b;
           
           cin >> a >> b;
           tree[a].push_back(b);
           tree[b].push_back(a);
       }
       
       queue<int> q;
       parents[1] = 0;
       visited[1] = true;
       q.push(1);
       
       while(!q.empty()){
           int x = q.front(); q.pop();
           for(int y : tree[x]){
               if(!visited[y]){
                   visited[y] = true;
                   parents[y] = x;
                   q.push(y);
               }
           }
       }
       
       for(int i = 2; i <= cnt ; i++)
           cout << parents[i] << "\n";
       return 0;
   }
   
   ```

8. 14503 - 로봇 청소기

   [site](https://www.acmicpc.net/problem/14503)

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 2 초      | 512 MB      | 17532 | 8904 | 5791      | 50.139%   |

   ## 문제

   로봇 청소기가 주어졌을 때, 청소하는 영역의 개수를 구하는 프로그램을 작성하시오.

   로봇 청소기가 있는 장소는 N×M 크기의 직사각형으로 나타낼 수 있으며, 1×1크기의 정사각형 칸으로 나누어져 있다. 각각의 칸은 벽 또는 빈 칸이다. 청소기는 바라보는 방향이 있으며, 이 방향은 동, 서, 남, 북중 하나이다. 지도의 각 칸은 (r, c)로 나타낼 수 있고, r은 북쪽으로부터 떨어진 칸의 개수, c는 서쪽으로 부터 떨어진 칸의 개수이다.

   로봇 청소기는 다음과 같이 작동한다.

   1. 현재 위치를 청소한다.
   2. 현재 위치에서 현재 방향을 기준으로 왼쪽방향부터 차례대로 탐색을 진행한다.
      1. 왼쪽 방향에 아직 청소하지 않은 공간이 존재한다면, 그 방향으로 회전한 다음 한 칸을 전진하고 1번부터 진행한다.
      2. 왼쪽 방향에 청소할 공간이 없다면, 그 방향으로 회전하고 2번으로 돌아간다.
      3. 네 방향 모두 청소가 이미 되어있거나 벽인 경우에는, 바라보는 방향을 유지한 채로 한 칸 후진을 하고 2번으로 돌아간다.
      4. 네 방향 모두 청소가 이미 되어있거나 벽이면서, 뒤쪽 방향이 벽이라 후진도 할 수 없는 경우에는 작동을 멈춘다.

   로봇 청소기는 이미 청소되어있는 칸을 또 청소하지 않으며, 벽을 통과할 수 없다.

   ## 입력

   첫째 줄에 세로 크기 N과 가로 크기 M이 주어진다. (3 ≤ N, M ≤ 50)

   둘째 줄에 로봇 청소기가 있는 칸의 좌표 (r, c)와 바라보는 방향 d가 주어진다. d가 0인 경우에는 북쪽을, 1인 경우에는 동쪽을, 2인 경우에는 남쪽을, 3인 경우에는 서쪽을 바라보고 있는 것이다.

   셋째 줄부터 N개의 줄에 장소의 상태가 북쪽부터 남쪽 순서대로, 각 줄은 서쪽부터 동쪽 순서대로 주어진다. 빈 칸은 0, 벽은 1로 주어진다. 장소의 모든 외곽은 벽이다.

   로봇 청소기가 있는 칸의 상태는 항상 빈 칸이다.

   ## 출력

   로봇 청소기가 청소하는 칸의 개수를 출력한다.

   ## 예제 입력 1 복사

   ```
   3 3
   1 1 0
   1 1 1
   1 0 1
   1 1 1
   ```

   ## 예제 출력 1 복사

   ```
   1
   ```

   ## 예제 입력 2 복사

   ```
   11 10
   7 4 0
   1 1 1 1 1 1 1 1 1 1
   1 0 0 0 0 0 0 0 0 1
   1 0 0 0 1 1 1 1 0 1
   1 0 0 1 1 0 0 0 0 1
   1 0 1 1 0 0 0 0 0 1
   1 0 0 0 0 0 0 0 0 1
   1 0 0 0 0 0 0 1 0 1
   1 0 0 0 0 0 1 1 0 1
   1 0 0 0 0 0 1 1 0 1
   1 0 0 0 0 0 0 0 0 1
   1 1 1 1 1 1 1 1 1 1
   ```

   ## 예제 출력 2 복사

   ```
   57
   ```

   ```c++
   //
   //  로봇청소기 (14503).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 12/05/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   // 핵심 포인트, 처음에 dx, dy를 어떤 순서대로 넣어 줄 것인가!
   #include <iostream>
   #include <queue>
   #include <algorithm>
   using namespace std;
   int arr[101][101];
   bool visited[101][101];
   int N, M, r,c,d;
   //int dx[] = {0, 1, 0, -1}; // 북,동,남,서
   //int dy[] = {1, 0, -1, 0};
   int dx[] = {-1, 0, 1, 0}; // 서, 북, 동, 남
   int dy[] = {0, 1, 0, -1};
   int cnt = 0;
   
   int directionNext(int d){
       // 북->서, 서->남, 남->동, 동->북
       if(d == 0)
           return 3;
       else if(d == 3)
           return 2;
       else if(d == 2)
           return 1;
       else
           return 0;
   }
   int directionBack(int d){
       // 북->남, 남->북, 동->서, 서->동
       if(d == 0)
           return 2;
       else if(d == 1)
           return 3;
       else if(d == 2)
           return 0;
       else
           return 1;
   }
   void BFS(int a, int b, int d){
       //0 N, 1 E, 2 S, 3 W
       cnt += 1;
       
       queue<pair<int,int>> que;
       que.push(make_pair(a,b));
       visited[a][b]= true;
       int next = d;
       while(!que.empty()){
           int x = que.front().first;
           int y = que.front().second;
           bool go = false;
           que.pop();
           for(int i = 0 ; i < 4 ; i++){
               // 여기서 방향을 정해줘야함
               next = directionNext(next);
               int nx = x + dx[next];
               int ny = y + dy[next];
               //움직일지 여부
               if(nx >= 0 && ny >= 0 && nx < N && ny < M ){
                   if(arr[nx][ny] == 0 && !visited[nx][ny]){
                       go = true;
                       visited[nx][ny] = true;
                       que.push(make_pair(nx,ny));
                       cnt += 1;
                       break;
                   }
               }
           }
           if(go == false){
               int back = directionBack(next);
               int bx = x + dx[back];
               int by = y + dy[back];
   //            cout << "back " << back << " next " << next << endl;
   //            cout <<"x,y (" << x <<" , " << y << ") " <<"bx, by (" << bx << ", " << by << ") arr[bx][by] : " <<  arr[bx][by] << endl;
               if(arr[bx][by] == 1)
                   break;
               
               que.push(make_pair(bx,by));
   
           }
       }
   }
   int main()
   {
       ios_base::sync_with_stdio();
       cin.tie(0);
       cout.tie(0);
       cin >> N >> M >>  r >> c >> d;
       
       for(int i = 0 ; i < N ; i ++){
           for(int j = 0 ; j < M ; j++){
               cin >> arr[i][j];
           }
       }
       BFS(r,c,d);
   
       cout << cnt << endl;
       return 0;
   }
   
   ```

9. 아기 상어

   [site](https://www.acmicpc.net/problem/16236)

   | 시간 제한 | 메모리 제한 | 제출  | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :---- | :--- | :-------- | :-------- |
   | 2 초      | 512 MB      | 13906 | 5474 | 3099      | 36.497%   |

   ## 문제

   N×N 크기의 공간에 물고기 M마리와 아기 상어 1마리가 있다. 공간은 1×1 크기의 정사각형 칸으로 나누어져 있다. 한 칸에는 물고기가 최대 1마리 존재한다.

   아기 상어와 물고기는 모두 크기를 가지고 있고, 이 크기는 자연수이다. 가장 처음에 아기 상어의 크기는 2이고, 아기 상어는 1초에 상하좌우로 인접한 한 칸씩 이동한다.

   아기 상어는 자신의 크기보다 큰 물고기가 있는 칸은 지나갈 수 없고, 나머지 칸은 모두 지나갈 수 있다. 아기 상어는 자신의 크기보다 작은 물고기만 먹을 수 있다. 따라서, 크기가 같은 물고기는 먹을 수 없지만, 그 물고기가 있는 칸은 지나갈 수 있다.

   아기 상어가 어디로 이동할지 결정하는 방법은 아래와 같다.

   - 더 이상 먹을 수 있는 물고기가 공간에 없다면 아기 상어는 엄마 상어에게 도움을 요청한다.
   - 먹을 수 있는 물고기가 1마리라면, 그 물고기를 먹으러 간다.
   - 먹을 수 있는 물고기가 1마리보다 많다면, 거리가 가장 가까운 물고기를 먹으러 간다.
     - 거리는 아기 상어가 있는 칸에서 물고기가 있는 칸으로 이동할 때, 지나야하는 칸의 개수의 최솟값이다.
     - 거리가 가까운 물고기가 많다면, 가장 위에 있는 물고기, 그러한 물고기가 여러마리라면, 가장 왼쪽에 있는 물고기를 먹는다.

   아기 상어의 이동은 1초 걸리고, 물고기를 먹는데 걸리는 시간은 없다고 가정한다. 즉, 아기 상어가 먹을 수 있는 물고기가 있는 칸으로 이동했다면, 이동과 동시에 물고기를 먹는다. 물고기를 먹으면, 그 칸은 빈 칸이 된다.

   아기 상어는 자신의 크기와 같은 수의 물고기를 먹을 때 마다 크기가 1 증가한다. 예를 들어, 크기가 2인 아기 상어는 물고기를 2마리 먹으면 크기가 3이 된다.

   공간의 상태가 주어졌을 때, 아기 상어가 몇 초 동안 엄마 상어에게 도움을 요청하지 않고 물고기를 잡아먹을 수 있는지 구하는 프로그램을 작성하시오.

   ## 입력

   첫째 줄에 공간의 크기 N(2 ≤ N ≤ 20)이 주어진다.

   둘째 줄부터 N개의 줄에 공간의 상태가 주어진다. 공간의 상태는 0, 1, 2, 3, 4, 5, 6, 9로 이루어져 있고, 아래와 같은 의미를 가진다.

   - 0: 빈 칸
   - 1, 2, 3, 4, 5, 6: 칸에 있는 물고기의 크기
   - 9: 아기 상어의 위치

   아기 상어는 공간에 한 마리 있다.

   ## 출력

   첫째 줄에 아기 상어가 엄마 상어에게 도움을 요청하지 않고 물고기를 잡아먹을 수 있는 시간을 출력한다.

   ## 예제 입력 1 복사

   ```
   3
   0 0 0
   0 0 0
   0 9 0
   ```

   ## 예제 출력 1 복사

   ```
   0
   ```

   ## 예제 입력 2 복사

   ```
   3
   0 0 1
   0 0 0
   0 9 0
   ```

   ## 예제 출력 2 복사

   ```
   3
   ```

   ## 예제 입력 3 복사

   ```
   4
   4 3 2 1
   0 0 0 0
   0 0 9 0
   1 2 3 4
   ```

   ## 예제 출력 3 복사

   ```
   14
   ```

   ## 예제 입력 4 복사

   ```
   6
   5 4 3 2 3 4
   4 3 2 3 4 5
   3 2 9 5 6 6
   2 1 2 3 4 5
   3 2 1 6 5 4
   6 6 6 6 6 6
   ```

   ## 예제 출력 4 복사

   ```
   60
   ```

   ## 예제 입력 5 복사

   ```
   6
   6 0 6 0 6 1
   0 0 0 0 0 2
   2 3 4 5 6 6
   0 0 0 0 0 2
   0 2 0 0 0 0
   3 9 3 0 0 1
   ```

   ## 예제 출력 5 복사

   ```
   48
   ```

   ## 예제 입력 6 복사

   ```
   6
   1 1 1 1 1 1
   2 2 6 2 2 3
   2 2 5 2 2 3
   2 2 2 4 6 3
   0 0 0 0 0 6
   0 0 0 0 0 9
   ```

   ## 예제 출력 6 복사

   ```
   39
   ```

   ```c++
   //
   //  아기상어 (16236) - new.cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 06/06/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   
   #include <iostream>
   #include <queue>
   #include <algorithm>
   #include <vector>
   #include <cstring>
   using namespace std;
   
   int N;
   int arr[101][101];
   int dist[101][101];
   int d;
   int x,y;
   int s_size = 2;
   int dx[] = {0, 0, 1, -1};
   int dy[] = {1, -1, 0, 0};
   vector<pair<int,int>> eat;
   pair<int, int> last;
   
   void BFS(int a, int b){
       eat.clear();
       d = 1000000;
       memset(dist, 0, sizeof(dist));
       queue<pair<int,int>> q;
       q.push(make_pair(a,b));
       while(!q.empty()){
           int x = q.front().first;
           int y = q.front().second;
           q.pop();
           for(int i = 0 ; i < 4; i++){
               int nx = x + dx[i];
               int ny = y + dy[i];
               
               if(nx >=0 && ny >=0 && nx < N && ny < N){
                   if(dist[nx][ny]==0 && arr[nx][ny] <= s_size){
                       dist[nx][ny] = dist[x][y]+1;
                       if(arr[nx][ny] > 0 && arr[nx][ny] < s_size){
                           if(d >= dist[nx][ny]){
                               eat.push_back(make_pair(nx, ny));
                               d = dist[nx][ny];
                               last.first = nx;
                               last.second = ny;
                           }
                       }
                       q.push(make_pair(nx,ny));
                   }
               }
           }
       }
   }
   
   int main()
   {
       ios_base::sync_with_stdio();
       cin.tie(0);
       cout.tie(0);
       
       cin >> N;
       for(int i = 0 ; i < N ; i++){
           for(int j = 0 ; j < N; j++){
               cin >> arr[i][j];
               if(arr[i][j] == 9){
                   x = i;
                   y = j;
                   arr[i][j] = 0;
               }
           }
       }
       int cnt= 0;
       int result=0;
       while(true){
           BFS(x,y);
           if(eat.empty()){
               break;
           }
           else{
               if(eat.size()==1){
                   x = last.first;
                   y = last.second;
   //                continue;
               }
               else{
                   for(int i = 0 ; i < eat.size();i++){
                       int cx = eat[i].first;
                       int cy = eat[i].second;
                       if(dist[cx][cy] == d){
                           if(last.first == cx){
                               if(last.second > cy ){
                                   last = eat[i];
                               }
                           }else if(last.first > cx){
                               last = eat[i];
                           }
                       }
                   }
               }
               cnt++;
               x = last.first;
               y = last.second;
               arr[x][y]= 0;
               result += dist[x][y];
               if(cnt == s_size){
                   s_size++;
                   cnt=0;
               }
           }
       }
       
       cout << result << "\n";
       
       return 0;
   }
   
   ```

10. s

    ```c++
    
    ```

11. s

    ```c++
    
    ```

12. s

    ```c++
    
    ```

13. s

    ```c++
    
    ```

14. s

    ```c++
    
    ```

15. s

    ```c++
    
    ```

16. s

    ```c++
    
    ```

17. s

    ```c++
    
    ```

18. s

    ```c++
    
    ```

19. s

    ```c++
    
    ```

20. s

    ```c++
    
    ```

    