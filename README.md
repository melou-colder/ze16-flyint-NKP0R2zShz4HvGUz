
* > 比赛链接 [https://sim.csp.thusaac.com/contest/36/home](https://github.com)


 


* > 比赛感受


这会刚打完上海icpc，比起区域赛的题，这个简单太多了。
感受还不错，写的很顺手。除了第3题，其他3题都是一发过。
刷题得长期刷。
 


 
![](https://img2024.cnblogs.com/blog/3466055/202412/3466055-20241223132749783-538930337.png)
 
 
 
 


* > A题 移动


 


题意：f : y\+1 ;  b : y\-1 ;   l : x\-1 ;  r : x\+1
 
 
一个简单的模拟，若当前操作使机器人移出场地，那么使机器人移回来就好
 



```


|  | #include |
| --- | --- |
|  | #define int long long |
|  | using namespace std; |
|  | void ooo(int x){ |
|  | cout<'\n'; |
|  | } |
|  | signed main() |
|  | { |
|  | int n, k;cin>>n>>k; |
|  | for(int i=1;i<=k;i++){ |
|  | int x, y;cin>>x>>y; |
|  | string s;cin>>s; |
|  | int len=s.size(); |
|  | for(int j=0;j |
|  | if(s[j]=='f')y+=1; |
|  | else if(s[j]=='b')y-=1; |
|  | else if(s[j]=='l')x-=1; |
|  | else x+=1; |
|  |  |
|  | if(y>n)y--; |
|  | if(y<1)y++; |
|  | if(x>n)x--; |
|  | if(x<1)x++; |
|  | } |
|  | cout<' '<'\n'; |
|  | } |
|  | return 0; |
|  | } |
|  |  |


```

 


* > B题 梦境巡查


 


这个题不算太难，有点思维，对码力要求不高。


  


它假设当bi为0时求初始时要带的最小补给。


关键在于怎样维护bi\=0时，全程中所拥有补给的最小量（为负数表示还需要多少补给）
所以就是一个单点修改，以bi为分界处，维护前半段和后半段最小值，对两段最小值取最小值，为负数则取绝对值，为非负数则为0。


 
 
![](https://img2024.cnblogs.com/blog/3466055/202412/3466055-20241223142520436-1013043504.jpg)


 



```


|  | #include |
| --- | --- |
|  | #define int long long |
|  | using namespace std; |
|  | const int xmmm=2e5+10; |
|  | int a[xmmm], b[xmmm]; |
|  | int c[xmmm]; |
|  | int sum[xmmm]; |
|  | int pmi[xmmm], lmi[xmmm]; |
|  | int ans[xmmm]; |
|  | void ooo(int x){ |
|  | cout<'\n'; |
|  | } |
|  | signed main() |
|  | { |
|  | int n;cin>>n; |
|  | for(int i=0;i<=n;i++){ |
|  | cin>>a[i]; |
|  | c[i*2+1]=0-a[i]; |
|  | } |
|  | for(int i=1;i<=n;i++){ |
|  | cin>>b[i]; |
|  | c[i*2]=b[i]; |
|  | } |
|  | pmi[0]=lmi[2*n+2]=0-1e10; |
|  | for(int i=1;i<=2*n+1;i++){ |
|  | sum[i]=sum[i-1]+c[i]; |
|  | } |
|  | for(int i=1;i<=2*n+1;i++){ |
|  | if(i==1)pmi[i]=sum[i]; |
|  | else pmi[i]=min(pmi[i-1], sum[i]); |
|  | } |
|  | for(int i=2*n+1;i>=1;i--){ |
|  | if(i==2*n+1)lmi[i]=sum[i]; |
|  | else lmi[i]=min(lmi[i+1], sum[i]); |
|  | } |
|  | for(int i=1;i<=n;i++){ |
|  | int pos=i*2; |
|  | int t1=pmi[pos-1]; |
|  | int t2=lmi[pos]-b[i]; |
|  | ans[i]=min(t1, t2); |
|  | } |
|  | for(int i=1;i<=n;i++){ |
|  | if(ans[i]<0)cout<<0-ans[i]<<' '; |
|  | else cout<<0<<' '; |
|  | } |
|  | return 0; |
|  | } |
|  | /* |
|  |  |
|  | 3 |
|  | 5 5 5 5 |
|  | 0 100 0 |
|  |  |
|  | 3 |
|  | 9 4 6 2 |
|  | 9 4 6 |
|  | */ |
|  |  |


```

 


* > D题 跳房子


这个题感觉还没有C题难。
这其实是一个很简单的图遍历的问题
建完边还是只有一个前驱的这种，简单版的迪杰斯特拉。
处理出b数组，每个点只入队列一次。
 


![](https://img2024.cnblogs.com/blog/3466055/202412/3466055-20241223145649343-19681653.png)


 


![](https://img2024.cnblogs.com/blog/3466055/202412/3466055-20241223145729093-1099311156.jpg)


 



```


|  | #include |
| --- | --- |
|  | //#define int long long |
|  | using namespace std; |
|  | void ooo(int x){ |
|  | cout<'\n'; |
|  | } |
|  | struct p{ |
|  | int id, num; |
|  | }; |
|  | const int xmmm=2e5+10; |
|  | int a[xmmm], b[xmmm], k[xmmm]; |
|  | int dis[xmmm]; |
|  | bool vis[xmmm]; |
|  | signed main() |
|  | { |
|  | int n;cin>>n; |
|  | for(int i=1;i<=n;i++){ |
|  | cin>>a[i]; |
|  | b[i]=i-a[i]; |
|  | } |
|  | for(int i=1;i<=n;i++)cin>>k[i]; |
|  | int pos=0; |
|  | queueq; |
|  | //q.clear(); |
|  | q.push(p{1, 0}); |
|  | int ans=-1; |
|  | while(!q.empty()){ |
|  | p t=q.front();q.pop(); |
|  | if(vis[t.id])continue; |
|  | vis[t.id]=1; |
|  | if(t.id==n){ |
|  | ans=t.num;break; |
|  | } |
|  | int x=t.id; |
|  | if(x+k[x]<=pos)continue; |
|  | if(x+k[x]>=n){ |
|  | q.push(p{n, t.num+1}); |
|  | continue; |
|  | } |
|  | for(int i=max(pos+1, x+1);i<=min(n, x+k[x]);i++){ |
|  | q.push(p{b[i], t.num+1}); |
|  | } |
|  | pos=max(pos, x+k[x]); |
|  | } |
|  | cout<'\n'; |
|  | return 0; |
|  | } |
|  | /* |
|  |  |
|  | 5 |
|  | 0 1 2 3 0 |
|  | 3 4 4 10 15 |
|  |  |
|  | 10 |
|  | 0 1 1 1 1 3 1 0 3 0 |
|  | 2 4 5 4 1 4 1 3 5 3 |
|  | */ |
|  |  |


```

 


* > C题 缓存模拟


 
一个大模拟按他的要求来就好了，详细的可以看注释
 



```


|  | #include |
| --- | --- |
|  | #define int long long |
|  |  |
|  | using namespace std; |
|  | const int xxx=3e5; |
|  | const int xx=7e4; |
|  | int head[xxx],nnum[xxx]; |
|  |  |
|  | // m组里有多少个 |
|  | struct p{ |
|  | int x, y; |
|  | }; |
|  | vectorans; |
|  | void ooo(int x){ |
|  | cout<<x<<'\n'; |
|  | }; |
|  | struct node { |
|  | int id, num; |
|  | bool operator<(const node &a)const {return a.num |
|  | }; |
|  | priority_queueqq[xx]; |
|  | unordered_map<int, int>a, vis; // 位置//是否修改 |
|  | signed main() |
|  | { |
|  |  |
|  | int n, m, q;cin>>n>>m>>q; |
|  | for(int i=1;i<=q;i++){ |
|  | int x, y;cin>>x>>y; |
|  | if(a[y]){ / /判断是否命中 |
|  | int pos=(y / n ) %m; |
|  | head[pos]++; |
|  | qq[pos].push(node{y, head[pos]}); |
|  | a[y]=head[pos]; |
|  | if(x==0)x=x; |
|  | else { |
|  | vis[y]=1; //判断是否改写 |
|  | } |
|  | } |
|  | else { |
|  | int pos=( y / n )%m; //位置 |
|  | if(nnum[pos]==n){ //如果已经满了 |
|  | while(!qq[pos].empty()){ |
|  | node tt=qq[pos].top();qq[pos].pop(); |
|  | if(a[tt.id]!=tt.num)continue; |
|  | if(vis[tt.id]){ |
|  | //cout<<"pos"<' '<' '<'\n'; |
|  | ans.push_back(p{(int)1, tt.id}); |
|  | vis[tt.id]=0; |
|  | } |
|  | head[pos]++; |
|  | a[y]=head[pos]; |
|  | if(x)vis[y]=1; |
|  | qq[pos].push(node{y, head[pos]}); |
|  | ans.push_back(p{(int)0, y}); |
|  | a[tt.id]=0;break; |
|  | } |
|  | } |
|  | else { |
|  | head[pos]++; |
|  | a[y]=head[pos]; |
|  | nnum[pos]++; |
|  | qq[pos].push(node{y, head[pos]}); |
|  | if(x)vis[y]=1; |
|  | ans.push_back(p{(int)0, y}); |
|  | } |
|  | } |
|  | } |
|  | int len=ans.size(); |
|  | for(int i=0;i |
|  | cout<' '<'\n'; |
|  | } |
|  | return 0; |
|  | } |
|  | /* |
|  |  |
|  | 4 8 8 |
|  | 0 0 |
|  | 0 1 |
|  | 1 2 |
|  | 0 1 |
|  | 1 0 |
|  | 0 32 |
|  | 1 33 |
|  | 0 34 |
|  |  |
|  |  |
|  | 1 1 3 |
|  | 1 0 |
|  | 1 1 |
|  | 0 2 |
|  | */ |
|  |  |


```

 


 


* > 自我总结


这次写题的顺序是1243，再写一点点。


 本博客参考[豆荚加速器官网PodHub](https://doujiaa.com)。转载请注明出处！
