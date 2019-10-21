# Tree





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

