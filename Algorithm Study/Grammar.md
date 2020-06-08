# Map

### Sort a map by values in C++
#### 1. Using std::vector

```c++

#include <iostream>
#include <map>
#include <vector>
#include <algorithm>

typedef std::pair<std::string, int> pair;

int main()
{
    std::map<std::string, int> map = {{"1", 1}, {"2", 2}};
    
    std::vector<pair> vec;
    
    std::copy(map.begin(), map.end(), std::back_inserter<std::vector<pair>>(vec));
    
    
    std::sort(vec.begin(), vec.end(), [](const pair& l, const pair& r){
       if(l.second != r.second)
           return l.second < r.second;
       return l.first < r.first;
       });
       
     return 0;
}
```

#### 2. Using std::set

```c++

#include <iostream>
#include <map>
#include <set>

struct comp
{
  template<typename T>
  bool operator()(const T& l, const T& r) const
  {
    if(l.second != r.second)
        return l.second < r.second;
     return l.first < r.first;
   }
 };
 
 int main()
 {
    std::map<std::string, int> map = {{"1", 1}, {"2", 2}};
    
    std::set<std::pair<std::string, int>, comp> set(map.begin(), map.end());
    
    return 0;
  }
  
```


#### 3.Using std::multimap

``` c++

#include <iostream>
#include <map>
#include <set>
#include <algorithm>

template<typename K, typename V>
std::multimap<V,K> invertMap(std::map<K,V> const &map)
{
    std:: multimap<V,K> multimap;
    
    for(auto const & pair: map)
    {
        multimap.insert(std::makr_pair(pair.second, pair.first));
     }
     
     return multimap;
 }
 
 int main()
 {
     std::map<std::string, int> map = {{"1", 1}, {"2", 2}};
     
     //invert the map
     std::multimap<int, std::string> multimap = invertMap(map);
     
     
     return 0;
} 

```

