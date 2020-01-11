# Cash

1. cash - 캐시

   [Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200105.md)

   [문제사이트](https://programmers.co.kr/learn/courses/30/lessons/17680)

   지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.
   이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.
   어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.

   어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.

   ### 입력 형식

- 캐시 크기(`cacheSize`)와 도시이름 배열(`cities`)을 입력받는다.
- `cacheSize`는 정수이며, 범위는 0 ≦ `cacheSize` ≦ 30 이다.
- `cities`는 도시 이름으로 이뤄진 문자열 배열로, 최대 도시 수는 100,000개이다.
- 각 도시 이름은 공백, 숫자, 특수문자 등이 없는 영문자로 구성되며, 대소문자 구분을 하지 않는다. 도시 이름은 최대 20자로 이루어져 있다.

### 출력 형식

- 입력된 도시이름 배열을 순서대로 처리할 때, 총 실행시간을 출력한다.

### 조건

- 캐시 교체 알고리즘은 `LRU`(Least Recently Used)를 사용한다.
- `cache hit`일 경우 실행시간은 `1`이다.
- `cache miss`일 경우 실행시간은 `5`이다.

[Original MD](/Users/yeokyuli/Google Drive/KyuLi/구글/Data-Structure/Algorithm Study/20200105.md)

```c++
#include <string>
#include <vector>
#include <iostream>
#include <cctype>
#include <algorithm>
#include <string>
#include <deque>
#include <iterator>

/*
가장 오랫동안 사용되지 않은 것을 제거
0. cacheSize == 0 -> vector size * 5
1. deque, vector, linked list ? -> deque 선택 : key를 사용하지 않으니 unordered_map (hash)를 사용할 필요 없음
-> cacheSize 만큼 deque 생성
-> small case로 input,
-> uses를 파악하면서 만약 deque에 없으면 오래 사용한 것을 pop하고 push_front로 새로 넣어줌 +5
-> 있으면 앞으로 swap +1

*/

using namespace std;

int solution(int cacheSize, vector<string> cities) {
    int answer = 0;
    deque<string> dq;
    if(cacheSize==0)
        return cities.size() * 5;
    
    for(auto& val : cities)
    {
        transform(val.begin(), val.end(), val.begin(), ::tolower);
        auto it = find_if(dq.begin(), dq.end(), [val](string& tmp){ return tmp == val;});
        if(it != dq.end())
        {
            auto id = distance(dq.begin(), it);
            dq.erase(dq.begin()+id);
            answer += 1;
        }
        else if(dq.size() <= cacheSize)
        {
            if(dq.size() == cacheSize)
                dq.pop_back();
            answer += 5;
        }
        dq.push_front(val);
    }
    
    return answer;
}
```



2. LRU Cache - Medium

   [site](https://leetcode.com/problems/lru-cache/)

   Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

   `get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
   `put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

   The cache is initialized with a **positive** capacity.

   **Follow up:**
   Could you do both operations in **O(1)** time complexity?

   **Example:**

   ```
   LRUCache cache = new LRUCache( 2 /* capacity */ );
   
   cache.put(1, 1);
   cache.put(2, 2);
   cache.get(1);       // returns 1
   cache.put(3, 3);    // evicts key 2
   cache.get(2);       // returns -1 (not found)
   cache.put(4, 4);    // evicts key 1
   cache.get(1);       // returns -1 (not found)
   cache.get(3);       // returns 3
   cache.get(4);       // returns 4
   ```

    

   ```c++
   class LRUCache {
       
   public:
       LRUCache(int capacity) : _capacity(capacity) {}
       
       int get(int key) {
           if (cache.find(key) != cache.end()) {
               use(key);
               return cache[key];
           }
           return -1;
       }
       void put(int key, int value) {
           use(key);
           cache[key] = value;
       }
   
   private:
       int _capacity;
       list<int> recent;
       unordered_map<int, int> cache;
       unordered_map<int, list<int>::iterator> pos;
       
       void use(int key)
       {
           if(pos.find(key) != pos.end())
               recent.erase(pos[key]);
           else if(cache.size() == _capacity)
           {
               cache.erase(recent.back());
               pos.erase(recent.back());
               recent.pop_back();
           }
           recent.push_front(key);
           pos[key] = recent.begin();
       }
   };
   
   /**
    * Your LRUCache object will be instantiated and called as such:
    * LRUCache* obj = new LRUCache(capacity);
    * int param_1 = obj->get(key);
    * obj->put(key,value);
    */
   ```

   