# Linked List

I referenced the [greeksforgeeks](https://www.geeksforgeeks.org/data-structures/linked-list/)

This Linked List is based on Singly Linked List.



* Principles of Linked List

  ​	A linked list is a linear data structure, in which the lements are not stored at **contiguous memory locations.**

  - Advantages over Arrays

    1. Dynamic size

    2. Ease of Insertion / deletion

  - Drawbacks

    1. Random access is not allowed.
    2. Extra memory space for a pointer is required with each element of the list.
    3. Not cached friendly. Since array elements are contiguous locations, there is locality of reference which is not there is case of linked lists.

  - ss

    

  ![img](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist.png)



* **Insert**

  * At the front of the linked list (**push_front()**)

    ![linkedlist_insert_at_start](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_at_start.png)

  * After a give node (**insert_after()**)

    ![linkedlist_insert_middle](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_middle.png)

  * At the end of the linked list (**push_back()**)

    ![linkedlist_insert_last](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_last.png)

* **Delete**

  * At the front of the linked list (**pop_front()**)
  * After a give node (**erase_after()**)
    	1. Find previous node of the node to be deleted.
     	2. Chnage the next of previous node.
     	3. Freee memory for the node to be deleted.
  * At the end of the linked list (**pop_back()**)

![linkedlist_deletion](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/05/Linkedlist_deletion.png)

```c++
#include <iostream>
using namespace std;
struct Node
{
public:
    int val;
    Node* next = nullptr;
    Node(int x) : val(x), next(nullptr){}
};

class LinkedList
{
private:
    Node *head, *tail;
public:
    LinkedList() : head(nullptr), tail(nullptr){}
    
    void create(int inputValue)
    {
        Node* node = new Node(inputValue);
        
        if(head == nullptr)
        {
            head = node;
            tail = node;
        }
        else
        {
            tail->next = node;
            tail = node;
        }
        
    }
    
    void disply()
    {
        Node* temp = head;
        while(temp)
        {
            cout << temp->val << " ";
            temp = temp->next;
        }
        cout << endl;
        delete temp;
    }
    
    void push_front(int inputValue)
    {
        Node* temp = new Node(inputValue);
        
        temp->next = head;
        head = temp;
    }
    
    void pop_front()
    {
        Node* temp = head->next;
        head = temp;
        
    }
    
    void insert_after(int index, int inputValue)
    {
        Node* newNode = new Node(inputValue);
        Node* cur = head;
        Node* pre;
        for(int i = 1 ; i < index; i++)
        {
            pre = cur;
            cur = cur->next;
        }
        pre->next = newNode;
        newNode->next = cur;
        
        
    }
    
    void erase_after(int index)
    {
        Node* cur = head;
        Node* pre;
        for(int i = 1; i < index; i++)
        {
            pre = cur;
            cur = cur->next;
        }
        pre->next = cur->next;
        delete cur;
    }
    
    void push_back(int inputValue)
    {
        Node* node = new Node(inputValue);
        tail->next = node;
        tail = node;
        
    }
    
    void pop_back()
    {
        Node* temp = head;
        while(temp->next->next != nullptr)
        {
            temp = temp->next;
        }
        
        tail = temp;
        tail->next = nullptr;
 
    }
};

int main()
{
    
    LinkedList list;
    
    list.create(20);
    list.create(2);
    list.create(100);
    list.push_front(1);
    list.pop_front();
    list.disply();
    list.insert_after(2, 10);
    list.erase_after(3);
    list.push_back(1);
    list.disply();
    list.pop_back();
    list.disply();

    return 0;
}
```



* **Leetcode code solutions**

  [Linked List](https://leetcode.com/problemset/all/?search=linked list)



* **Frequently Problems**
  * Singly Linked List
    * [Find Length of a Linked List (Iterative and Recursive)](http://geeksquiz.com/find-length-of-a-linked-list-iterative-and-recursive/)
    * [Nth node from the end of a Linked List](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)
    * [Function to check if a singly linked list is palindrome](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)
    * [Remove duplicates from an unsorted linked list](https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/)
    * [Swap nodes in a linked list without swapping data](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)
    * [Intersection of two Sorted Linked Lists](https://www.geeksforgeeks.org/intersection-of-two-sorted-linked-lists/)
    * [QuickSort on Singly Linked List](https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)
    * [Reverse a linked list](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)
  * Circular Linked List
    * [Circular Linked List Traversal](http://geeksquiz.com/circular-linked-list-set-2-traversal/)
    * [Sorted insert for circular linked list](https://www.geeksforgeeks.org/sorted-insert-for-circular-linked-list/)
    * [Convert a Binary Tree to a Circular Doubly Link List](https://www.geeksforgeeks.org/convert-a-binary-tree-to-a-circular-doubly-link-list/)
    * [Circular Singly Linked List | Insertion](https://www.geeksforgeeks.org/circular-singly-linked-list-insertion/)
    * [Deletion from a Circular Linked List](https://www.geeksforgeeks.org/deletion-circular-linked-list/)
    * [Convert singly linked list into circular linked list](https://www.geeksforgeeks.org/convert-singly-linked-list-circular-linked-list/)
  * Doubly Linked List
    * [Doubly Linked List Introduction and Insertion](http://geeksquiz.com/doubly-linked-list/)
    * [Delete a node in a Doubly Linked List](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)
    * [Reverse a Doubly Linked List](https://www.geeksforgeeks.org/reverse-a-doubly-linked-list/)
    * [QuickSort on Doubly Linked List](https://www.geeksforgeeks.org/quicksort-for-linked-list/)
    * [Swap Kth node from beginning with Kth node from end in a Linked List](https://www.geeksforgeeks.org/swap-kth-node-from-beginning-with-kth-node-from-end-in-a-linked-list/)
    * [Merge Sort for Doubly Linked List](https://www.geeksforgeeks.org/merge-sort-for-doubly-linked-list/)



1. Add Two Numbers

   [site](https://leetcode.com/problems/add-two-numbers/)

   You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

   You may assume the two numbers do not contain any leading zero, except the number 0 itself.

   **Example:**

   ```
   Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
   Output: 7 -> 0 -> 8
   Explanation: 342 + 465 = 807.
   ```

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   #include <iostream>
   #include <cstdlib>
   class Solution {
   public:
       ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
           ListNode* dummy = new ListNode(0);
           ListNode* node = dummy;
           int sum,c=0;
           
           while(l1||l2){
               int x = (l1 != NULL) ? l1->val : 0;
               int y = (l2 != NULL) ? l2->val : 0;
               sum = x + y + c;
               c = 0;
               if(sum>=10)
                   c = 1;
               node->next = new ListNode(sum%10);;
               node = node->next;
               if(l1 != NULL) l1 = l1->next;
               if(l2 != NULL) l2 = l2->next;
           }
           if(c==1){
               node->next = new ListNode(1);;
               node = node->next;
           }
           node = dummy->next;
           delete dummy;
           return node;
       
       }
   };
   ```

   

2. Remove Nth Node From End of List - Medium

   [site](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

   Given a linked list, remove the *n*-th node from the end of list and return its head.

   **Example:**

   ```
   Given linked list: 1->2->3->4->5, and n = 2.
   
   After removing the second node from the end, the linked list becomes 1->2->3->5.
   ```

   **Note:**

   Given *n* will always be valid.

   **Follow up:**

   Could you do this in one pass?

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   class Solution {
   public:
       ListNode* removeNthFromEnd(ListNode* head, int n) {
           ListNode* tmp = head;
           int cnt=0;
           while(tmp != nullptr){
               cnt++;
               tmp = tmp->next;
           }
           if(cnt == n)
               return head->next;
           
           int remove = cnt - n;
           tmp = head;
           while(--remove){
               tmp = tmp->next;
           }
           tmp->next = tmp->next->next;        
           return head;
       }
   };
   ```

   

3. Merge Two Sorted Lists - Easy

   Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

   **Example:**

   ```
   Input: 1->2->4, 1->3->4
   Output: 1->1->2->3->4->4
   ```

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   class Solution {
   public:
       ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
           ListNode* result = new ListNode(0);
           
           
           
           while(l1)
           {
               result->next = l1;
               l1 = l1->next;
               result = result->next;
               // if(l1->val < l2->val){
               //     result->next = l1;
               //     l1 = l1->next;
               // }
               // else
               // {               
               //     ListNode* tmp= new ListNode(l2->val);
               //     result->next = tmp;
               //     result = tmp;
               //     l2 = l2->next;
               // }
               
           }
           
           return result;
       }
   };
   ```

   

4. Linked List Cycle - Easy

   [Site](https://leetcode.com/problems/linked-list-cycle/)

   Given a linked list, determine if it has a cycle in it.

   To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

   **Example 1:**

   ```
   Input: head = [3,2,0,-4], pos = 1
   Output: true
   Explanation: There is a cycle in the linked list, where tail connects to the second node.
   ```

   ![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   #include <iostream>
   using namespace std;
   class Solution {
   public:
       bool hasCycle(ListNode *head) {
           ListNode *slow = new ListNode(0);
           ListNode *fast = new ListNode(0);
           slow = head; fast = head;
           while(fast != NULL && fast->next != NULL){
               slow = slow->next;
               fast = fast->next->next;
               // cout << slow->val << " " << fast->val << endl;
               if(slow == fast)
                   return true;
           }      
           
           return false;
       }
   };
   ```

   

5. Intersection of Two Linked Lists - Easy

   [site](https://leetcode.com/problems/intersection-of-two-linked-lists/)

   Write a program to find the node at which the intersection of two singly linked lists begins.

   For example, the following two linked lists:

   [![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)

    

   **Example 1:**

   [![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

    

   **Example 2:**

   [![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

    

   **Example 3:**

   [![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

    

   **Notes:**

   - If the two linked lists have no intersection at all, return `null`.
   - The linked lists must retain their original structure after the function returns.
   - You may assume there are no cycles anywhere in the entire linked structure.
   - Your code should preferably run in O(n) time and use only O(1) memory.

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   #include <iostream>
   using namespace std;
   
   class Solution {
   public:
       ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
           ListNode* a = headA;
           ListNode* b = headB;
           
           if(headA == NULL or headB == NULL)
               return NULL;
           
           while(a != b){
               a = (a != NULL) ? a->next : headB;
               b = (b != NULL) ? b->next : headA;
           }
           return a;
       }
   };
   ```

   

6. Reverse Linked List - Easy

   [site](https://leetcode.com/problems/reverse-linked-list/)

   **Example:**

   ```
   Input: 1->2->3->4->5->NULL
   Output: 5->4->3->2->1->NULL
   ```

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   #include <iostream>
   using namespace std;
   class Solution {
   public:
       ListNode* reverseList(ListNode* head) {
           ListNode* newNode = NULL;
           ListNode* cur = head;
           
           while(cur != NULL){
               ListNode* temp = cur->next;
               cur->next = newNode;
               newNode = cur;  
               cur = temp;
           }
           
           return newNode;
       }
   };
   ```

   

7. Palindrome Linked List - Easy

   Given a singly linked list, determine if it is a palindrome.

   **Example 2:**

   ```
   Input: 1->2->2->1
   Output: true
   ```

   

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   #include <stack>
   using namespace std;
   class Solution {
   public:
       bool isPalindrome(ListNode* head) {
           ListNode* h = head;
           stack<int> s;
           while(h){
               s.push(h->val);
               h = h->next;
           }
           while(head){
               if(head->val != s.top())
                   return false;
               s.pop();
               head = head->next;
           }
           return true;
       }
   };
   ```

   

8. Delete Node in a Linked List

* ```c++
  /**
   * Definition for singly-linked list.
   * struct ListNode {
   *     int val;
   *     ListNode *next;
   *     ListNode(int x) : val(x), next(NULL) {}
   * };
   */
  class Solution {
  public:
      void deleteNode(ListNode* node) {
          node->val = node->next->val;
          node->next = node->next->next;
      }
  };
  ```

  

9. Odd Even Linked List - Medium

   Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

   You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

   **Example 1:**

   ```
   Input: 1->2->3->4->5->NULL
   Output: 1->3->5->2->4->NULL
   ```

   **Example 2:**

   ```
   Input: 2->1->3->5->6->4->7->NULL
   Output: 2->3->6->7->1->5->4->NULL
   ```

   **Note:**

   - The relative order inside both the even and odd groups should remain as it was in the input.
   - The first node is considered odd, the second node even and so on ...

   ```c++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
   class Solution {
   public:
       ListNode* oddEvenList(ListNode* head) {
           if(head == NULL)
               return NULL;
           ListNode* odd = head;
           ListNode* even = head->next;
           ListNode* evenHead = even; 
           int cnt = 1;
           while(even and even->next){
               odd->next = even->next;
               odd = odd->next;
               even->next = odd->next;
               even = even->next;
           }
           odd->next = evenHead;
           
           return head;
       }
   };
   ```

10.  Delete Node in a Linked List - Easy

    Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

    Given linked list -- head = [4,5,1,9], which looks like following:

    ![img](https://assets.leetcode.com/uploads/2018/12/28/237_example.png)

     

    **Example 1:**

    ```
    Input: head = [4,5,1,9], node = 5
    Output: [4,1,9]
    Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
    ```

    **Example 2:**

    ```
    Input: head = [4,5,1,9], node = 1
    Output: [4,5,9]
    Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.
    ```

     

    **Note:**

    - The linked list will have at least two elements.
    - All of the nodes' values will be unique.
    - The given node will not be the tail and it will always be a valid node of the linked list.
    - Do not return anything from your function.

    ```c++
    /**
     * Definition for singly-linked list.
     * struct ListNode {
     *     int val;
     *     ListNode *next;
     *     ListNode(int x) : val(x), next(NULL) {}
     * };
     */
    class Solution {
    public:
        void deleteNode(ListNode* node) {
            node->val = node->next->val;
            node->next = node->next->next;
        }
    };
    ```

    