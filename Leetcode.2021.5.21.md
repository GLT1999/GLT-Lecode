```c++
/*
任务调度器
题意：不同类型相邻需要另外加时等待n秒，求至少需要的时间
解法：暴力
*/
class Solution{
    public:
    int leastInterval(vector<char>&tasks,int n){
        int count[26]={0},maxnum=-1,samewithmax=0,len=tasks.size();
        for(char c: tasks) count[c-'A']++;
        for(int i=0;i<26;i++){
            if(count[i]>maxnum){
                maxnum=count[i];
                samewithmax=-1;
            }
            if(count[i]==maxnum) samewithmax++;
        }
        return max((maxnum-1)*n+maxnum+samewithmax,len);
    }
}
```

```c++
/*
PTA浪漫侧影
题意：已知二叉树中后序求二叉树左右视图
*/
#include<bits/stdc++.h>
using namespace std;
const int N=1e6+10;
const int INF=0x3f3f3f3f;
int pre[N],mid[N],post[N],n;
struct node{
    int val;
    node *l,*r;
};
vector<int>v[2];
struct node *create_by_pre_mid(int len,int pre[],int mid[]){
    if(len<=0) return NULL;
    int i;struct node *T;
    T=new node;
    T->val=pre[0];
    for(i=0;i<len;i++) if(pre[0]==mid[i]) break;
    T->l=create_by_pre_mid(i,pre+1,mid);
    T->r=create_by_pre_mid(len-i-1,pre+i+1,mid+i+1);
    return T;
}
struct node *create_by_mid_post(int len,int post[],int mid[]){
    if(len<=0) return NULL;
    int i;struct node *T;
    T=new node;
    T->val=post[len-1];
    for(i=0;i<len;i++) if(post[len-1]==mid[i]) break;
    T->l=create_by_mid_post(i,post,mid);
    T->r=create_by_mid_post(len-i-1,post+i,mid+i+1);
    return T;
}
void left_right_view(node *T){
    queue<node*>q;
    q.push(T);
    if(T==NULL) cout<<"NULL"<<endl;
    int m=1;
    while(!q.empty()){
        int count=0;
        for(int i=0;i<m;i++){
            node *x=q.front();q.pop();
            if(i==0) v[0].push_back(x->val);
            if(i==m-1)v[1].push_back(x->val);
            if(x->l){
                q.push(x->l);
                count++;
            }
            if(x->r){
                q.push(x->r);
                count++;
            }
        }
        m=count;
    }
}
int main(){
    cin>>n;
    for(int i=0;i<n;i++) cin>>mid[i];
    for(int i=0;i<n;i++) cin>>post[i];
    struct node *T;
    T=create_by_mid_post(n,post,mid);
    left_right_view(T);
    cout<<"R:";
    for(auto x:v[1]) cout<<x<<" ";
    cout<<endl<<"L:";
    for(auto x:v[0]) cout<<x<<" ";
}
```

```c++
/*
PTA：矩阵列平移
题解：指定偶数列下移1~k位，空位补x
解法：模拟
*/
using namespace std;
const int N=101;
const int INF=0x3f3f3f3f;
int n,k,x,G[N][N];
vector<int>v;
int main(){
	cin>>n>>k>>x;
	int res=n/2;
	for(int i=1;i<=n;i++){
		for(int j=1;j<=n;j++){
			cin>>G[i][j];
		}
	}
	int sign=1;
	for(int i=1;i<=res;i++){
		for(int j=n;j>sign;j--){
			G[j][i*2]=G[j-sign][i*2];
		}
		for(int j=1;j<=sign;j++){
			G[j][i*2]=x;
		}
		if(sign==k){
			sign=1;
			continue;
		}
		sign++;
	}
	for(int i=1;i<=n;i++){
		int sum=0;
		for(int j=1;j<=n;j++){
			sum+=G[i][j];
		}
		v.push_back(sum);
	}
	for(int i=0;i<v.size();i++){
		if(i==v.size()-1) cout<<v[i];
		else cout<<v[i]<<" ";
	}
} 
```

```c++
/*
PTA：约会大作战
考察：模拟
*/
#include<bits/stdc++.h>
using namespace std;
const int N=101;
int n,m,k,flag,x,y;
struct people_o{
    int res=0;		//拒绝过人数
    int favor[101];  //对另一组每个人好感度
    int down[501];	 //对已拒绝人的好感度
    int partner;
}A[N];
struct people_t{
    int res=0;
    int favor[101];
    int down[501];
    int partner;
}B[N];
void Scanf(){
    cin>>n>>m>>k;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>A[i].favor[j];
        }
    }
    for(int i=1;i<=m;i++){
        for(int j=1;j<=n;j++){
            cin>>B[i].favor[j];
        }
    }
}
int main(){
    Scanf();
    for(int i=1;i<=k;i++){
        cin>>x>>y;
        if((A[x].res>=2&&B[y].res>=2)&&
		(!A[x].partner&&!B[y].partner)&&
		(A[x].favor[y]>A[x].down[A[x].res]&&A[x].favor[y]>A[x].down[A[x].res-1])&&
		(B[y].favor[x]>B[y].down[B[y].res]&&B[y].favor[x]>B[y].down[B[y].res-1]))
		{
            A[x].partner=y;B[y].partner=x;
            flag=1;
            cout<<x<<" "<<y<<endl;
        }
        else{
            A[x].down[A[x].res++]=A[x].favor[y];
            B[y].down[B[y].res++]=B[y].favor[x];
        }
    }
    if(!flag) cout<<"PTA is my only love"<<endl;
}
```

