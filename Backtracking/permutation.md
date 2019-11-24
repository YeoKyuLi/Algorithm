# Permutation

1. permutation

Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```c++

class Solution {
public:
    void premutation(vector<int>& per, int begin, vector<vector<int>>& output)
    {
        if(begin == per.size() ){
            output.push_back(per);
            return ;
        }
        for(int i = begin; i < per.size(); i++)
        {
            swap(per[begin], per[i]);
            premutation(per, begin+1, output);
            swap(per[begin], per[i]);          
        }
        
    }
    
    vector<vector<int>> permute(vector<int>& nums) {   
        vector<vector<int>> output;

        premutation(nums, 0,output);
        
        
        return output;
    }
};


```



2. permutation 2

   Given a collection of numbers that might contain duplicates, return all possible unique permutations.

   **Example:**

   ```
   Input: [1,1,2]
   Output:
   [
     [1,1,2],
     [1,2,1],
     [2,1,1]
   ]
   ```

   ```c++
   class Solution {
   public:
       void permu(vector<int>& nums, int begin, vector<vector<int>>& output)
       {
           if(begin >= nums.size())
           {
               if(find(output.begin(), output.end(), nums) == output.end())
                   output.push_back(nums);
           }
           for(int i = begin; i < nums.size(); i++)
           {
               swap(nums[begin], nums[i]);
               permu(nums, begin+1, output);
               swap(nums[begin], nums[i]);
           }
       }
       vector<vector<int>> permuteUnique(vector<int>& nums) {
           vector<vector<int>> result;
           permu(nums, 0, result);
           
           return result;
       }
   };
   ```

   

3. Next Permutation

   Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

   If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

   The replacement must be **[in-place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

   Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

   ```
   1,2,3` → `1,3,2`
   `3,2,1` → `1,2,3`
   `1,1,5` → `1,5,1
   ```