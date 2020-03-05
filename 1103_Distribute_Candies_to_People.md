> 题目描述：把糖candies分给n个人，给第一个人一颗糖，第二个人两颗糖。。。，
>
> 然后把n+1颗糖给第一个人，n+2颗糖给第二个人。。。。，2n颗糖给第n个人，
>
> 重复这个过程直到把糖分完，返回每个人分的糖数。

eg:

```java
Input: candies = 7, num_people = 4
Output: [1,2,3,1]
Explanation:
On the first turn, ans[0] += 1, and the array is [1,0,0,0].
On the second turn, ans[1] += 2, and the array is [1,2,0,0].
On the third turn, ans[2] += 3, and the array is [1,2,3,0].
On the fourth turn, ans[3] += 1 (because there is only one candy left), and the final array is [1,2,3,1].
```

> 思路描述：其实我们可以注意到这是一个循环，然后也不需要太麻烦计算

```C++
class Solution {
public:
    vector<int> distributeCandies(int candies, int num_people) {
        vector<int> num(num_people, 0);
        if(num_people == 0)
            return num;
        if(num_people == 1){
            num[0] = candies;
            return num;
        }
        int sum = 0, i = 0;
        while(1){
            sum += i + 1;
            if(sum > candies){
                num[i % num_people] += candies + i + 1 - sum;
                break;
            }else
                num[i % num_people] += i + 1;
            i += 1;
        }
        return num;
    }
};
```
