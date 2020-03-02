> 题目描述：给定非空字符串s和包含一系列单词的字典，判断s是否能分成单词
>
> 注意：相同的单词可以重复使用多次，假设字典中不包含重复的单词

eg:

```java
Example 1:

Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
    
Example 2:

Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
    
Example 3:

Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

> 思路描述：这里我们就用一个一维的 dp 数组，其中 dp[i] 表示范围 [0, i) 内的子串是否可以拆分，注意这里 dp 数组的长度比s串的长度大1，是因为我们要 handle 空串的情况，我们初始化 dp[0] 为 true，然后开始遍历。注意这里我们需要两个 for 循环来遍历，因为此时已经没有递归函数了，所以我们必须要遍历所有的子串，我们用j把 [0, i) 范围内的子串分为了两部分，[0, j) 和 [j, i)，其中范围 [0, j) 就是 dp[j]，范围 [j, i) 就是 s.substr(j, i-j)，其中 dp[j] 是之前的状态，我们已经算出来了，可以直接取，只需要在字典中查找 s.substr(j, i-j) 是否存在了，如果二者均为 true，将 dp[i] 赋为 true，并且 break 掉，此时就不需要再用j去分 [0, i) 范围了，因为 [0, i) 范围已经可以拆分了。最终我们返回 dp 数组的最后一个值，就是整个数组是否可以拆分的布尔值了，代码如下：

```C++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
        vector<int> memo(s.size(), -1);
        return check(s, wordSet, 0, memo);
    }
    bool check(string s, unordered_set<string>& wordSet, int start, vector<int>& memo) {
        if (start >= s.size()) return true;
        if (memo[start] != -1) return memo[start];
        for (int i = start + 1; i <= s.size(); ++i) {
            if (wordSet.count(s.substr(start, i - start)) && check(s, wordSet, i, memo)) {
                return memo[start] = 1;
            }
        }
        return memo[start] = 0;
    }
};
```
> 这个就比较清晰了
```C++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
        vector<bool> dp(s.size() + 1);
        dp[0] = true;
        for (int i = 0; i < dp.size(); ++i) {
            for (int j = 0; j < i; ++j) {
                if (dp[j] && wordSet.count(s.substr(j, i - j))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp.back();
    }
};
```



set操作：

```C++
unordered_set代表是无序的，
set<int> numSet;
    for(int i=0;i<6;i++)
    {
        //2.1insert into set
        numSet.insert(numList[i]);
    }
    //2.travese set
    for(set<int>::iterator it=numSet.begin() ;it!=numSet.end();it++)
    {
        cout<<*it<<" occurs "<<endl;
    }
    //3.set find useage

    int findNum=1;
    if(numSet.find(findNum)!=numSet.end())
    {
        cout<<"find num "<<findNum<<" in set"<<endl;
    }else{
        cout<<"do not find num in set"<<findNum<<endl;
    }
    //set delete useage
    int eraseReturn=numSet.erase(1);
    if(1==eraseReturn)
    {
          cout<<"erase num 1 success"<<endl;
    }else{
        cout<<"erase failed,erase num not in set"<<endl;
    }
```



C++字符串操作：

```
1.string类型的声明： 
string s;

2.string类型的初始化:    
string s="abcd";   或者   string s="a  b   cd";
这两种分别是不带空格和带空格的初始化，是都可以的。

3.string类型的读入:
cin>>s;             //不能读入空格，以空格、制表符、回车符作为结束标志
getline(cin,s);   //可以读入空格和制表符，以回车符作为结束标志

4.求string类型的长度：
int len=s.size();    或者     int len=s.length();
两种方法是等价的

5.求string类型下标为i的字符:
s[i]        或        char c=s.at(i)

6.查找t是否为s的子串:
s.find(t);
如果t是s的子串则返回首次匹配的位置，否则返回 string::npos 或 -1

7.字符数组转string类型:
s=str;
str为char数组，s为string类型

8.string类型转字符数组:
strcpy(str,s.c_str());
需要引用string.h头文件

9.两个string比较大小：
if(s1<s2);       或       s1.compare(s2);
相等时返回0；s1>s2时返回1，s1<s2时返回-1

10.两个string连接：
s1=s1+s2;        或       s1.append(s2);

11.对string类型数组排序
string s[100];
sort(s,s+n,cmp);
int cmp(string a,string b)
{
    return a<b; //或a>b;
}

12. 字符串提取
   str2 = str1.substr();
   str2 = str1.substr(pos1);
   str2 = str1.substr(pos1,len1);
   string a=s.substr(0,4);       //获得字符串s中 从第0位开始的长度为4的字
 
符串
 
13. 字符串搜索
   where = str1.find(str2);
   where = str1.find(str2,pos1); pos1是从str1的第几位开始。
   where = str1.rfind(str2); 从后往前搜。
 
14. 插入字符串
   不是赋值语句。
   str1.insert(pos1,str2);
   str1.insert(pos1,str2,pos2,len2);
   str1.insert(pos1,numchar,char);    numchar是插入次数，char是要插入的字
符。
 
15. 替换字符串
   str1.replace(pos1,str2);
   str1.replace(pos1,str2,pos2,len2);
 
16. 删除字符串
   str.erase(pos,len)
   str.clear();
 
17. 交换字符串
   swap(str1,str2);
```

