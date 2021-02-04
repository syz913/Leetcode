### 题目描述

用一维数组存储学号和成绩，然后，按成绩排序输出。

#### 输入描述

>```c++
>输入第一行包括一个整数N(1<=N<=100)，代表学生的个数。
>接下来的N行每行包括两个整数p和q，分别代表每个学生的学号和成绩。
>```

#### 输出描述

>```c++
>按照学生的成绩从小到大进行排序，并将排序后的学生信息打印出来。
>如果学生的成绩相同，则按照学号的大小进行从小到大排序。
>```

### 示例

输入：

```c++
3
1 90
2 87
3 92
```

输出：

```c++
2 87
1 90
3 92
```

### 思路

这个和上面的成绩排序其实一样，但是要简单很多，这个就采用重载运算符的做法了。重载运算符可以参考一下我的博客 https://blog.csdn.net/sinat_41895958/article/details/113369584

```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

class Student{
public:
    int code;
    int grade;
public:
    Student(int code, int grade):code(code),grade(grade){}
    bool operator <(const Student& stu)const {
        return stu.grade == grade ? code < stu.code : grade < stu.grade;
    }
};

int main(){
    int n;
    while(cin >> n){
        vector<Student> students;
        for(int i = 0; i < n; i ++){
            int code; int grade;
            cin >> code >> grade;
            students.emplace_back(code, grade);
        }
        sort(students.begin(), students.end());
        for(Student stu : students){
            cout << stu.code << " " << stu.grade << endl;
        }
    }
    return 0;
}
```
