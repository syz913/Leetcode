### 题目描述

查找和排序 

输入任意（用户，成绩）序列，可以获得成绩从高到低或从低到高的排列，相同成绩都按先录入排列在前的规则处理。 

### 示例

```c++
jack   70
peter   96
Tom    70
smith   67 

从高到低 成绩 
peter   96 
jack   70 
Tom    70 
smith   67 

从低到高 
smith   67 
jack   70 
Tom   70 
peter   96 
```

### 思路

排序很简单，重点是相同成绩按照录入顺序进行排列，这时候有两种方法，一种是构建 Student 类的时候也加入每个成绩的 index，这样成绩相同的时候比较 index 就好了，也可以直接用 stable_sort

```c++
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>

using namespace std;

class Student{
public:
    string name;
    int grade;
public:
    Student(string name, int grade):name(name),grade(grade){}
};

bool lessCmp(Student a, Student b){
    return a.grade < b.grade;
}

bool greaterCmp(Student a, Student b){
    return a.grade > b.grade;
}

int main(){
    int n, type;
    while(cin >> n >> type){
        vector<Student> students;
        for(int i = 0; i < n; i ++){
            string name; int grade;
            cin >> name >> grade;
            students.emplace_back(name, grade);
        }
        if(type == 0) stable_sort(students.begin(), students.end(), greaterCmp);
        else stable_sort(students.begin(), students.end(), lessCmp);
        for(Student stu : students){
            cout << stu.name << " " << stu.grade << endl;
        }
    }
    return 0;
}
```
