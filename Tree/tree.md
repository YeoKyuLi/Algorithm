# Binary Tree Data Structure

A tree whose elements have at most 2 children is called a binary tree.

Unlike Arrays, Linked Lists, Stack and queues which are linear data structures, trees are hierarchical data structures.

![img](https://media.geeksforgeeks.org/wp-content/cdn-uploads/binary-tree-to-DLL.png)

##### Why Trees?

1. To store information that naturally froms a hierarchy.
2. It's provide moderate access/search (quicker than Linked List and slower than arrays)
3. It's provide moderate insertion/deletion (quicker than Arrays and slower than Unordered Linked Lists).
4. Like Linked Lists and unlike Arrays, Trees don't have an upper limit on number of nodes as nodes are linked using pointers.



##### Types of Binary Tree

- Full Binary Tree : [Handshaking Lemma and Tree](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)

  ```
  - Every node has 0 or 2 children.
  - In a Full Binary, number of leaf nodes is number of internal nodes plus 1
  	L(Number of leaf nodes) = I(Number of internal nodes) + 1
            		18
             /       \  
           15         30  
          /  \        /  \
        40    50    100   40
        
  
               18
             /    \   
           15     20    
          /  \       
        40    50   
      /   \
     30   50
  
  ```

  

- Complete Binary Tree : [Binary Heap](https://www.geeksforgeeks.org/binary-heap/)

  ```
  - All levels are completely filled except possibly the last level and the last lavel has all keys as left as possible.
  
             18
             /       \  
           15         30  
          /  \        /  \
        40    50    100   40
  
  
                 18
             /       \  
           15         30  
          /  \        /  \
        40    50    100   40
       /  \   /
      8   7  9 
  ```

  

- Perfect Binary Tree

  ```
  - All internal nodes have two children and all leaves are at the same level.
  - Height h has 2^h -1 node.
                18
             /       \  
           15         30  
          /  \        /  \
        40    50    100   40
  
  
                 18
             /       \  
           15         30  
  ```

  

- Balanced Binary Tree : AVL tree, Red-Black tree

  [leetcode - Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

  ```
  - The representation example is AVL tree(Adelson-Velsky and Landis)
  - Height by making sure that the difference between heights of left and right subtress is atmost 1.
  
  
  ```

  ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/BinaryTreeRotations.svg/300px-BinaryTreeRotations.svg.png)

- A degenerate (or pathological) tree

  ```
  - Every internal node has one child.
  - Such trees are performancewise same as linked list.
        10
        /
      20
       \
       30
        \
        40  
  ```



![Image result for balanced binary tree](https://i.stack.imgur.com/MeMzS.png)

<img src="https://images.slideplayer.com/13/4168650/slides/slide_4.jpg" alt="Related image" style="zoom:50%;" />

https://www.geeksforgeeks.org/binary-tree-data-structure/





1. Tree traversal

```c++
/*
7
A B C
B D .
C E F
E . .
F . G
D . .
G . .

전위 순회한 결과 : ABDCEFG // (루트) (왼쪽 자식) (오른쪽 자식)
중위 순회한 결과 : DBAECFG // (왼쪽 자식) (루트) (오른쪽 자식)
후위 순회한 결과 : DBEGFCA // (왼쪽 자식) (오른쪽 자식) (루트)
*/
#include <iostream>

using namespace std;
int tree[26][2];
void preOrder(int node)
{
    if(node == int('.' - 'A'))
        return;
        
    cout << (char)(node + 'A');
    preOrder(tree[node][0]);
    preOrder(tree[node][1]);
}

void inOrder(int node)
{
    if(node == int('.' - 'A'))
        return;
        
    inOrder(tree[node][0]);
    cout << (char)(node + 'A');
    inOrder(tree[node][1]);
}


void postOrder(int node)
{
    if(node == int('.' - 'A'))
        return;

    postOrder(tree[node][0]);
    postOrder(tree[node][1]);
    cout << (char)(node + 'A');
}


int main()
{
    int cnt;
    
    cin >> cnt;
    
    char node, left, right;
    
    while(cnt--)
    {
        cin >> node >> left >> right;
        tree[node - 'A'][0] = left - 'A';
        tree[node - 'A'][1] = right - 'A';
    }
    
    preOrder(0);
    cout << endl;
    inOrder(0);
    cout << endl;
    postOrder(0);
    cout << endl;

    return 0;
```



2. Symmetric Tree - easy

   2. [site](https://leetcode.com/problems/symmetric-tree/)

      Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

      For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

      ```
          1
         / \
        2   2
       / \ / \
      3  4 4  3
      ```

       

      But the following `[1,2,2,null,3,null,3]` is not:

      ```
          1
         / \
        2   2
         \   \
         3    3
      ```

       

      **Note:**
      Bonus points if you could solve it both recursively and iteratively.

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
      class Solution {
      public:
          bool isSymmetric(TreeNode* root) {
              return traversal(root, root);
          }
      private:
          bool traversal(TreeNode* t1,TreeNode* t2)
          {
              // if(!t1 && !t2) return true;
              // if(!t1 || !t2) return false;
              if(t1 == nullptr || t2 == nullptr ) return t1 == t2;
              if(t1-> val != t2->val) return false;
              
              return/*(t1->val == t2->val) &&*/ traversal(t1->right, t2->left) && traversal(t1->left, t2->right);
          }
      };
      ```

3. Binary Tree Preorder Traversal - Medium

   [site](https://leetcode.com/problems/binary-tree-preorder-traversal/)

   Given a binary tree, return the *preorder* traversal of its nodes' values.

   **Example:**

   ```
   Input: [1,null,2,3]
      1
       \
        2
       /
      3
   
   Output: [1,2,3]
   ```

   **Follow up:** Recursive solution is trivial, could you do it iteratively?

4. ```c++
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
       
       vector<int> v;
       void preorder(TreeNode* head)
       {
           if(head == nullptr) return;
           
           v.push_back(head->val);
           preorder(head->left);
           preorder(head->right);
       }
       vector<int> preorderTraversal(TreeNode* root) {
           
           preorder(root);
           return v;
       }
   };
   ```



4. Binary Tree Postorder Traversal - Hard

   [site](https://leetcode.com/problems/binary-tree-postorder-traversal/)

   Given a binary tree, return the *postorder* traversal of its nodes' values.

   **Example:**

   ```
   Input: [1,null,2,3]
      1
       \
        2
       /
      3
   
   Output: [3,2,1]
   ```

   **Follow up:** Recursive solution is trivial, could you do it iteratively?

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
       vector<int> v;
       
       void postorder(TreeNode* head)
       {
           if(head == NULL) return;
           
           postorder(head->left);
           postorder(head->right);
           v.push_back(head->val);
       }
       vector<int> postorderTraversal(TreeNode* root) {
           postorder(root);
           return v;
       }
   };
   ```

5. Binary Tree Level Order Traversal - Medium

   [site](https://leetcode.com/problems/binary-tree-level-order-traversal/)

   Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

   For example:
   Given binary tree `[3,9,20,null,null,15,7]`,

   ```
       3
      / \
     9  20
       /  \
      15   7
   ```

   

   return its level order traversal as:

   ```
   [
     [3],
     [9,20],
     [15,7]
   ]
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
   //Solution1
   //     vector<vector<int>> res;
   //     void preOrder(TreeNode* root,int depth)
   //     {
   //         if(root == NULL) return;
           
   //         //It means pushing an empty array (NULL) while the depth becomes equal to the size of ret vector because in every other case if the tree is full, it is always greater than 1.
   //         //This means constructing an empty vector as the d-th(depth) element of the 2-d vector ret
   //         // if(res.size() == depth)
   //         //     res.push_back(vector<int>());
           
   //         if(res.size() == depth)
   //             res.resize(depth+1);
           
   //         res[depth].push_back(root->val);
   //         preOrder(root->left, depth+1);
   //         preOrder(root->right, depth+1);
   //     }
       // vector<vector<int>> levelOrder(TreeNode* root) {
       //     preOrder(root, 0);
       //     return res;
       // }
       
   // Solution2
   //     vector<vector<int>> levelOrder(TreeNode* root) {
   //         vector<vector<int>> res;
           
   //         if(!root)
   //             return res;
           
   //         queue<TreeNode*> que;
   //         que.push(root);
   //         que.push(NULL);
   //         vector<int> current_vector;
   //         while(!que.empty())
   //         {
   //             TreeNode* x = que.front();
   //             que.pop();
               
   //             if(x == NULL)
   //             {
   //                 res.push_back(current_vector);
   //                 current_vector.resize(0);
   //                 if (que.size() > 0) {
   //                     que.push(NULL);
   //                 }
                   
   //             }
   //             else
   //             {
   //                 current_vector.push_back(x->val);
   //                 if(x->left) que.push(x->left);
   //                 if(x->right) que.push(x->right);
   //             }
               
   //         }
           
   //         return res;
   //     }
       
       //Soltuion3
       vector<vector<int>> levelOrder(TreeNode* root) {
           
           vector<vector<int>> res;
           if(!root)
               return res;
           
           queue<TreeNode*> que;
           que.push(root);
           while(!que.empty())
           {
               int size = que.size();
               vector<int> current_vector;
               for(int i = 0 ; i < size; i++)
               {
                   TreeNode* x = que.front();
                   current_vector.push_back(x->val);
                   que.pop();
                   if(x->left)
                       que.push(x->left);
                   if(x->right)
                       que.push(x->right);
               }
               res.push_back(current_vector);
           }
           return res;
       }
   };
   ```

6. Binary Tree Inorder Traversal - Medium

   [site](https://leetcode.com/problems/binary-tree-inorder-traversal/)

   Given a binary tree, return the *inorder* traversal of its nodes' values.

   **Example:**

   ```
   Input: [1,null,2,3]
      1
       \
        2
       /
      3
   
   Output: [1,3,2]
   ```

   **Follow up:** Recursive solution is trivial, could you do it iteratively?

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
       vector<int> v;
       
       void inorder(TreeNode* head)
       {
           if(head == nullptr) return;
           
           inorder(head->left);
           v.push_back(head->val);
           inorder(head->right);
           
       }
       vector<int> inorderTraversal(TreeNode* root) {
   
           inorder(root);
           return v;
       }
   };
   ```

7. 2250 트리의 높이와 너비

   [site](https://www.acmicpc.net/problem/2250)

   | 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
   | :-------- | :---------- | :--- | :--- | :-------- | :-------- |
   | 2 초      | 128 MB      | 6351 | 1843 | 1285      | 27.405%   |

   ## 문제

   이진트리를 다음의 규칙에 따라 행과 열에 번호가 붙어있는 격자 모양의 틀 속에 그리려고 한다. 이때 다음의 규칙에 따라 그리려고 한다.

   1. 이진트리에서 같은 레벨(level)에 있는 노드는 같은 행에 위치한다.
   2. 한 열에는 한 노드만 존재한다.
   3. 임의의 노드의 왼쪽 부트리(left subtree)에 있는 노드들은 해당 노드보다 왼쪽의 열에 위치하고, 오른쪽 부트리(right subtree)에 있는 노드들은 해당 노드보다 오른쪽의 열에 위치한다.
   4. 노드가 배치된 가장 왼쪽 열과 오른쪽 열 사이엔 아무 노드도 없이 비어있는 열은 없다.

   이와 같은 규칙에 따라 이진트리를 그릴 때 각 레벨의 너비는 그 레벨에 할당된 노드 중 가장 오른쪽에 위치한 노드의 열 번호에서 가장 왼쪽에 위치한 노드의 열 번호를 뺀 값 더하기 1로 정의한다. 트리의 레벨은 가장 위쪽에 있는 루트 노드가 1이고 아래로 1씩 증가한다.

   아래 그림은 어떤 이진트리를 위의 규칙에 따라 그려 본 것이다. 첫 번째 레벨의 너비는 1, 두 번째 레벨의 너비는 13, 3번째, 4번째 레벨의 너비는 각각 18이고, 5번째 레벨의 너비는 13이며, 그리고 6번째 레벨의 너비는 12이다.

   ![img](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/upload/201008/ttt.PNG)

   우리는 주어진 이진트리를 위의 규칙에 따라 그릴 때에 너비가 가장 넓은 레벨과 그 레벨의 너비를 계산하려고 한다. 위의 그림의 예에서 너비가 가장 넓은 레벨은 3번째와 4번째로 그 너비는 18이다. 너비가 가장 넓은 레벨이 두 개 이상 있을 때는 번호가 작은 레벨을 답으로 한다. 그러므로 이 예에 대한 답은 레벨은 3이고, 너비는 18이다.

   임의의 이진트리가 입력으로 주어질 때 너비가 가장 넓은 레벨과 그 레벨의 너비를 출력하는 프로그램을 작성하시오

   ## 입력

   첫째 줄에 노드의 개수를 나타내는 정수 N(1 ≤ N ≤ 10,000)이 주어진다. 다음 N개의 줄에는 각 줄마다 노드 번호와 해당 노드의 왼쪽 자식 노드와 오른쪽 자식 노드의 번호가 순서대로 주어진다. 노드들의 번호는 1부터 N까지이며, 자식이 없는 경우에는 자식 노드의 번호에 -1이 주어진다.

   ## 출력

   첫째 줄에 너비가 가장 넓은 레벨과 그 레벨의 너비를 순서대로 출력한다. 너비가 가장 넓은 레벨이 두 개 이상 있을 때에는 번호가 작은 레벨을 출력한다.

   ## 예제 입력 1 복사

   ```
   19
   1 2 3
   2 4 5
   3 6 7
   4 8 -1
   5 9 10
   6 11 12
   7 13 -1
   8 -1 -1
   9 14 15
   10 -1 -1
   11 16 -1
   12 -1 -1
   13 17 -1
   14 -1 -1
   15 18 -1
   16 -1 -1
   17 -1 19
   18 -1 -1
   19 -1 -1
   ```

   ## 예제 출력 1 복사

   ```
   3 18
   ```

   ```c++
   //
   //  트리의 높이와 너비 (2250).cpp
   //  Algorithm_study
   //
   //  Created by Yeo Kyu Li on 29/04/2019.
   //  Copyright © 2019 Yeo Kyu Li. All rights reserved.
   //
   #include <iostream>
   #include <cstring>
   
   using namespace std;
   
   const int MAX = 10001;
   pair<int, int> tree[MAX];
   pair<int, int> minMax[MAX];
   int minX[MAX] = {10000};
   int maxX[MAX];
   int findNode[MAX];
   int x_coordinate = 1;
   int height;
   
   void DFS (int node, int level){
       
       
       if(tree[node].first > 0)
           DFS(tree[node].first, level+1);
       
   //    cout << " node : " << node <<  " level: " << level << " X : " << x_coordinate << endl;
   
       minX[level] = min(minX[level], x_coordinate);
       maxX[level] = max(maxX[level], x_coordinate);
       height = max(height, level);
   //    cout <<"level : " << level << " min: " << minX[level] << " max: " << maxX[level] << endl;
       
       x_coordinate++;
       
       if(tree[node].second > 0)
           DFS(tree[node].second, level+1);
               
   }
   int main()
   {
       
       int N;
       cin >> N;
       for(int i = 0 ; i < N; i++){
           int node, left, right;
           cin >> node >> left >> right;
           
           findNode[node]++;
           
           if(!tree[node].first)
               findNode[left]++;
           tree[node].first = left;
           
           if(!tree[node].second)
               findNode[right]++;
           
           tree[node].second = right;
       }
       
       int root = 0;
       for(int i = 1 ; i <= N ; i++){
           if(findNode[i] == 1)
               root = i;
       }
       fill_n(minX, MAX, MAX);
       DFS(root, 1);
       int sum, maxVal=0, levelNum=0;
       for(int i = 1 ; i <= height ; i++){
           sum = maxX[i] - minX[i] + 1;
           if(sum > maxVal){
               maxVal = sum;
               levelNum = i;
           }
       }
       
       cout << levelNum << " " << maxVal;
       return 0;
   }
   
   ```

8. d

   ```c++
   
   ```

9. d

   ```c++
   
   ```

   