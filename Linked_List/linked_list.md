# Linked List





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

