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





Tree traversal

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

















* **Leetcode**
  * [Tree](https://leetcode.com/tag/tree/)