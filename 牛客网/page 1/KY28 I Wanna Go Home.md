### 题目描述

The country is facing a terrible civil war----cities in the country are divided into two parts supporting different leaders. As a merchant, Mr. M does not pay attention to politics but he actually knows the severe situation, and your task is to help him reach home as soon as possible.   "For the sake of safety,", said Mr.M, "your route should contain at most 1 road which connects two cities of different camp."   Would you please tell Mr. M at least how long will it take to reach his sweet home?

#### 输入描述

>```c++
>The input contains multiple test cases.
>    The first line of each case is an integer N (2<=N<=600), representing the number of cities in the country.
>    The second line contains one integer M (0<=M<=10000), which is the number of roads.
>    The following M lines are the information of the roads. Each line contains three integers A, B and T, which means the road between city A and city B will cost time T. T is in the range of [1,500].
>    Next part contains N integers, which are either 1 or 2. The i-th integer shows the supporting leader of city i. 
>    To simplify the problem, we assume that Mr. M starts from city 1 and his target is city 2. City 1 always supports leader 1 while city 2 is at the same side of leader 2. 
>    Note that all roads are bidirectional and there is at most 1 road between two cities.
>Input is ended with a case of N=0.
>```

#### 输出描述

>```c++
>For each test case, output one integer representing the minimum time to reach home.
>    If it is impossible to reach home according to Mr. M's demands, output -1 instead.
>```

### 示例

输入：

```c++
2
1
1 2 100
1 2
3
3
1 2 100
1 3 40
2 3 50
1 2 1
5
5
3 1 200
5 3 150
2 5 160
4 3 170
4 2 170
1 2 2 2 1
0
```

输出：

```c++
100
90
540
```

### 思路

dijkstra

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<limits.h> 
using namespace std;
const int maxn=601;
struct graph{
    int to;
    int weight;
    graph(int t,int w):to(t),weight(w){}
    inline bool operator < (const graph &p)const{
        return weight<p.weight;
    }
};
struct Point{
    int index;
    int weight;//源点到index点的weight 
    Point(int i,int w):index(i),weight(w){}
    inline bool operator < (const Point &p)const{
        return weight>p.weight;
    }
};
int dis[maxn][2]; 
int leader[maxn];
vector<graph> g[maxn];
void init(){
    for(int i=0;i<maxn;i++){
        g[i].clear();
        dis[i][0]=dis[i][1]=INT_MAX;
        leader[i]=0;
    }
}
void dijkstra(int s,int l){  //l:0 or 1
    priority_queue<Point> q;
    dis[s][l]=0;
    q.push(Point(s,dis[s][l]));
    bool flag=true; 
    while(!q.empty()){
        int u=q.top().index;
        q.pop();
        if(u==2)continue; 
        for(int i=0;i<g[u].size();i++){
            int to=g[u][i].to;
            int weight=g[u][i].weight;
            int lead=abs(leader[u]-leader[to]);
            if(!(leader[u]==2&&leader[to]==1)){   //like:1 1 2 2 or 1 2 2 2 or 1 1 1 2
                if(dis[to][l]>dis[u][l]+weight){
                    dis[to][l]=dis[u][l]+weight;
                    q.push(Point(to,dis[to][l]));
                }
            }
        }
    }
}
int main(){
    int n,m,a,b,t;
    while(cin>>n){
        if(n==0)break;
        init();
        cin>>m;
        for(int i=0;i<m;i++){
            cin>>a>>b>>t;
            g[a].push_back(graph(b,t));
            g[b].push_back(graph(a,t));
        }
        for(int i=1;i<=n;i++){
            cin>>leader[i];
        }
        dijkstra(1,0);
        dijkstra(1,1);
        cout<<(min(dis[2][0],dis[2][1])==INT_MAX?-1:min(dis[2][0],dis[2][1]))<<endl;    
    }
    return 0;
}
```
