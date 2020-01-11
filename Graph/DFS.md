# DFS

1. DFS - 여행경로

   [Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200112.md)

   [site](https://programmers.co.kr/learn/courses/30/lessons/43164)

   ###### 문제 설명

   주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 ICN 공항에서 출발합니다.

   항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

   ##### 제한사항

- 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
- 주어진 공항 수는 3개 이상 10,000개 이하입니다.
- tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
- **주어진 항공권은 모두 사용해야 합니다.**
- 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
- 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.

```c++
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

/*
경로 리턴
항상 ICN 출발
가능한 경로가 2개 이상일 경우 알파벳 순서가 잎서는 경로 return
모든 경로를 반드시 방문 가능
DFS로 선택 
*/
using namespace std;

bool DFS(string from, vector<vector<string>>& tickets, vector<string>& answer, vector<int>& visited, int cnt)
{
    answer.push_back(from);

    for(int i = 0 ; i < tickets.size(); i++)
    {
        if(from == tickets[i][0] && visited[i] == 0)
        {
            visited[i] = 1;
            bool success = DFS(tickets[i][1], tickets, answer, visited, cnt+1);
            if(success) return true;
            else  visited[i] = 0;
        }
    }
    if(cnt == tickets.size()) return true;

    answer.pop_back();
    return false;
}

vector<string> solution(vector<vector<string>> tickets) {
    vector<string> answer;
    sort(tickets.begin(), tickets.end());
    vector<int> visited(tickets.size());
    DFS("ICN", tickets, answer, visited,0);
    return answer;
}
```



2. Same Tree - Easy

   [site](https://leetcode.com/problems/same-tree/)

   Given two binary trees, write a function to check if they are the same or not.

   Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

   **Example 1:**

   ```
   Input:     1         1
             / \       / \
            2   3     2   3
   
           [1,2,3],   [1,2,3]
   
   Output: true
   ```

   **Example 2:**

   ```
   Input:     1         1
             /           \
            2             2
   
           [1,2],     [1,null,2]
   
   Output: false
   ```

   **Example 3:**

   ```
   Input:     1         1
             / \       / \
            2   1     1   2
   
           [1,2,1],   [1,1,2]
   
   Output: false
   ```

3. ```c++
   /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
    * };
    */
   
   // inOrder or BFS 노 -> 왼 -> 오
   class Solution {
   public:
       bool isSameTree(TreeNode* p, TreeNode* q) {
   
           if(p==q)
               return true;
           if(q == nullptr || p == nullptr)
               return false;
           
           // if(BFS(p) == BFS(q))
           //     return true;
           vector<int> res1, res2;
           inOrder(p, res1);
           inOrder(q, res2);
           if(res1 == res2)
               return true;
           return false;
       }
   private:
       void inOrder(TreeNode* root, vector<int>& res)
       {
           if(root == nullptr)
               return;
           res.push_back(root->val);
           if(!root->left && root->right )
               res.push_back(NULL);
           inOrder(root->left, res);
           inOrder(root->right, res);
       }
   // private:
   //     vector<int> BFS(TreeNode* root)
   //     {
   //         vector<int> res;
           
   //         queue<TreeNode*> que;
   //         que.push(root);
   
   //         while(!que.empty())
   //         {
   //             int size = que.size();
   //             for(int i = 0; i < size; i++)
   //             {
   //                 TreeNode* cur = que.front();
   //                 que.pop();
   //                 res.push_back(cur->val);
   //                 if(cur->left)
   //                     que.push(cur->left);
   //                 if(!cur->left && cur->right )
   //                     res.push_back(NULL);
                   
   //                 if(cur->right)
   //                     que.push(cur->right);
   //             }
   //         }
           
   //         return res; 
   //     }
   };
   ```

4. Maximum Depth of Binary Tree - Easy

   [site](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

   Given a binary tree, find its maximum depth.

   The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

   **Note:** A leaf is a node with no children.

   **Example:**

   Given binary tree `[3,9,20,null,null,15,7]`,

   ```
       3
      / \
     9  20
       /  \
      15   7
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
   class Solution {
   public:
       //DFS, stack
       int maxDepth(TreeNode* root) {
           int depth = 0;
           if(root == nullptr)
               return depth;
           
           return max(maxDepth(root->left), maxDepth(root->right)) + 1;
           
       }
   };
   ```

5. s

   ```c++
   
   ```

6. s

   ```c++
   
   ```

7. s

   ```c++
   
   ```

8. s

   ```c++
   
   ```

9. s

   ```c++
   
   ```

   