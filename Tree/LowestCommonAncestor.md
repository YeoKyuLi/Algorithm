Lowest Common Ancestor
======================

The LCA of n1 and n2 in T is the shared ancestor of n1 and n2 that is located farthest from the root.

![](https://t1.daumcdn.net/cfile/tistory/996D16415A8A534A33)

##### Method 1

(By Storing root to n1 and root to n2 paths): Following is simple O(n) algorithm to find LCA of n1 and n2. 1) Find path from root to n1 and store it in a vector or array. 2) Find path from root to n2 and store it in another vector or array. 3) Traverse both paths till the values in arrays are same. Return the common element just before the mismatch.

https://code0xff.tistory.com/28 https://www.crocus.co.kr/660
