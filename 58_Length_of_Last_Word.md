> 题目描述：给定一个字符串s（包含大小写字母以及空格符），返回最后一个单词的长度，若不存在，返回0。

eg:

```java
Input: "Hello World"
Output: 5
```

> 思路描述：反向for循环，注意末尾为空格的情况即可。

```C++
class Solution {
public:
    int lengthOfLastWord(string s) {
        int n = s.size();
        if(n == 0)
            return 0;
        int length = 0;
        for(int i = n - 1; i >= 0; i --){
            if(s[i] != ' ') length ++;
            else if(length > 0) break;   
        }
        return length;
    }
};
```
