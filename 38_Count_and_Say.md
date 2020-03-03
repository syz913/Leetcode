> 题目描述：

eg:

```java
Example 1:

Input: 1
Output: "1"
Explanation: This is the base case.
Example 2:

Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
```

> 思路描述：比较容易理解的一种做法

```C++
class Solution {
public:
    string countAndSay(int n) {
        if(n <= 0) return "";
        if(n == 1) return "1";
        string res = "1";
        //循环n - 1次找到第n个数的读法
        for(int i = 0; i < n - 1; i ++){
            string cur = "";
            for(int j = 0; j < res.size(); j ++){
                int count = 1;//计数
                while(j + 1 < res.size() && res[j] == res[j + 1]){
                    j ++;
                    count ++;
                }
                cur += to_string(count) + res[j];
            }
            res = cur;
        }
        return res;
    }
};
```
