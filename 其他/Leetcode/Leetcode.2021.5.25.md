```c++
/*
找到字符串中所有字母异位词
题意：字母异位词指字母相同，但排列不同的字符串
解法：滑动窗口
*/
class Solution{
    public:
    vector<int>findAnagrams(string s,string p){
        vector<int>ans,res(128),window(128);
        if(p.size()>s.size()||s.size()==0) return ans;
        for(char x: p) res[x]++;
        for(int i=0;i<p.size()-1;i++) window[s[i]]++;
        int l=0,r=p.size()-1;
        while(r<s.size()){
            window[s[r++]]++;
            if(window==res) ans.push_back(l);
            window[s[l++]]--;
        }
        return ans;
    }
};
//超时
class Solution{
    public:
    vector<int>findAnagrams(string s,string p){
        int len=p.size();
        sort(p.begin(),p.end());
        vector<int>ans;
        for(int i=0;i<s.size();i++){
            string res=s.substr(i,len);
            sort(res.begin(),res.end());
            if(res==p) ans.push_back(i);
        }
        return ans;
    }
};
```

```c++
/*
路径总和 III
题意：找出路径和等于给定数值的路径总数，路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）
解法：DFS
*/
class Solution{
  public:
    int ans=0;
    int pathSum(TreeNode *root,int sum){
        if(root==NULL) return 0;
        DFS(root,sum);
        pathSum(root->left,sum);
        pathSum(root->right,sum);
        return ans;
    }
    void DFS(TreeNode *root,int s){
        if(root==NULL) return;
        if(root->val==s) ans++;
        DFS(root->left,s-root->val);
        DFS(root->right,s-root->val);
    }
};
```

