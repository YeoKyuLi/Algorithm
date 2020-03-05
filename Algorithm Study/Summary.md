[Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree) 



[Combinations](https://leetcode.com/problems/combinations) 

[Combination Sum IV](https://leetcode.com/problems/combination-sum-iv)  



[Coin Change](https://leetcode.com/problems/coin-change) 

[Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

[Decode Ways](https://leetcode.com/problems/decode-ways)

[Word Break](https://leetcode.com/problems/word-break)





[Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)





[Divide Two Integers](https://leetcode.com/problems/divide-two-integers) 

## Find target

```c++
vector<int> findTargetNum(vector<int>& v, int target)
{
	unordered_map<int,vector<int> m;
int sub;
for(int i = 0 ; i < v.size(); i++)
{
	sub = target - v[i];

	m[v[i]].push_back(i);
	m[sub].push_back(i);
	
	if(m[v[i]].size()-1 == 2)
		return m[v[i]];
}
	
	return {-1,-1};
}
```



```c++
vector<int> twoSum(vector<int>& nums, int target) {
   unordered_map<int, int> m;
   int sum = 0;

   for (int i = 0; i < nums.size(); i ++) {
      sum += nums[i];
      m[sum] = i;
      if (m.count(sum - target)) {
         return {i, m[sum-target]};
      }         
   }
   return {-1,-1};
}
```



### Find Squares

```c++
int dist(const pair<int,int>& p1, const pair<int,int>& p2){
	return pow( p2.first - p1.first, 2) + pow(p2.second - p1.second,2); 
}

bool validSquare(const vector<pair<int,int>>& points) {
	unordered_set<pair<int,int>> s;
	s.insert({dist(points[0], points[1]), dist(points[1], points[2]), dist(points[2], points[3]), dist(points[0], points[2]), dist(points[0], points[3]), dist(points[1],points[2])});
	return s.count() == 2;
}
```





#### Random Nums

```c++
       1   2  3   4  5  6  7
_________________ 
7| 0 7 14 21 28 35 42


rand7 -> rand49


1 ~ 49
int rand49() {
	return 7 * rand7() + rand7() ;
}

int rand40_49()
{
	int n = rand49();
	while( n <= 40) {
		n = rand49();
}
41 ~ 49;
return n;
}
int rand10() {
	return rand40_49() % 10+1;
}

```





#### Find Majority Number

```c++
int findMajorityElement(vector<int>& v)
{
	int cnt = 1, val = v[0];
	for(int i = 1; i < v.size(); i++)
	{
		if (val ==  v[i])
		 	cnt++;
		else
	cnt--;
if(cnt == 0)
	val = v[i];
	}
	if(cnt)
		return val;
else
	return -1;
}
```





#### Find Single Num

```c++
int findSingleNum(vector<int> & v)
{
	int res = 0;
	for(int i = 0 ; i < v.size(); i++)
	{
		res = res ^ v[i]; // res ^= v[i];
	}
	return res;
}
```



### Generate Parenthesis

```c++
class Solution {
public:
    vector<string> result;
    
    void generate(string str, int left, int right, int size)
    {
        if(str.length() == size*2)
            result.push_back(str);
        
        if(left < size)
            generate(str+"(", left+1, right, size);
        if(right < left)
            generate(str+")", left, right+1, size); 
        
        
    }
    
    vector<string> generateParenthesis(int n) {
        int right = 0, left = 0, size = n;
        generate("", left, right, size);        
        
        return result;
    }
};
```



```c++
void combination(vector<string>& res , int begin , int end, string tmp){
	if( begin == 0 && end == 0){
		res.push_back(tmp);
		return;
	}
	if (begin > 0)
		combination(res , begin-1 , end +1, tmp+”(“);
	if ( end > 0)
		combination(res , begin , end -1, tmp+”)”);
}

vector<string> makeParenthesis(int cnt)
{
	vector<string> res;	
	combination(res, cnt, 1, ““);
	return res;
}

```

