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
    * 