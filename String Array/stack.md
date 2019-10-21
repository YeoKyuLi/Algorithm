# Stack



```c++
*
2019.09.28
 Stack - array

*/
#include <iostream>

using namespace std;

class MinStack {
private:
    int arr[100];
    vector<int> st;
    stack<int> stack;
    int minNum = 100000;
    int location = 0;
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        arr[location] = x;
        location++;
        if(minNum > x){
            minNum = x;
        }
    }
    
    void pop() { // remove
        if(location <= 0)
            return;
        
        if(arr[location-1] == minNum){
            minNum = arr[0];
            for(int i = 1 ; i < location-1; i++)
            {
                if(minNum > arr[i])
                    minNum = arr[i];
            }
        }
        arr[location--];
    }
    
    int top() { //return
        if(location <= 0)
            return -1;
        return arr[location-1];
        
    }
    
    int getMin() {
        return minNum;
    }
};

int main()
{
    MinStack st;
    st.push(3);
    st.push(2);
    st.pop();
    cout << st.top() << endl;
    cout << st.getMin() << endl;

    return 0;
}
```



