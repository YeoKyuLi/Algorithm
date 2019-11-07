# Bit Manipulation



Leetcode 29. Divide Two Integers

Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing `dividend` by `divisor`.

The integer division should truncate toward zero.



```c++
class Solution {
public:
    int divide(int dividend, int divisor) {
        if (dividend == INT_MIN && divisor == -1) {
            return INT_MAX;
        }
        long result = 0;
        int sign = dividend > 0 ^ divisor > 0 ? -1 : 1;
        long dvd = labs(dividend), div = labs(divisor);

        
        while(dvd >= div)
        {
            long tmp = div, m = 1;
            while(tmp << 1 <= dvd) // right shift를 하면 *2, left shift 하면 /2
            {
                tmp <<= 1;
                m <<= 1;
            }
            dvd -= tmp;
            result += m;
        }
        
        // while(dvd >= div)
        // {
        //     dvd -= div;
        //     result++;
        // }
        
        return sign * result;
        
    }
};

int stringToInteger(string input) {
    return stoi(input);
}

int main() {
    string line;
    while (getline(cin, line)) {
        int dividend = stringToInteger(line);
        getline(cin, line);
        int divisor = stringToInteger(line);
        
        int ret = Solution().divide(dividend, divisor);

        string out = to_string(ret);
        cout << out << endl;
    }
    return 0;
}
```

