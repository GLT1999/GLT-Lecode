

```c++
/*
无重复字符的最长子串
题意：找出其中不含有重复字符的最长子串的长度
*/
//超时
class Solution {
public:
    int demo(string str){
        set<char>st;
        for(auto &x:str) st.insert(x);
        return st.size()==str.size();
    }
    int lengthOfLongestSubstring(string s) {
        int ans=0;
        for(int i=0;i<s.size();i++){
            for(int j=1;j<=s.size()-i;j++){
                string str=s.substr(i,j);
                int sign=str.size();
                if(demo(str)) ans=max(ans,sign);
            }
        }
        return ans;
    }
};
```

```c++
/*
二叉树的层次遍历
题意：给你一个二叉树，请你返回其按 层序遍历 得到的节点值
解法：BFS
*/
class Solution{
  public:
    vector<vector<int>> levelOrder(TreeNode *root){
        vector<vector<int>> v;
        if(!root) return v;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            int len=q.size();
            vector<int>t;
            for(int i=0;i<len;i++){
                TreeNode *x=q.front();q.pop();
                t.push_back(x->val);
                if(x->left) q.push(x->left);
                if(x->right)q.push(x->right);
            }
            v.push_back(t);
        }
        return v;
    }
};
```



```c++
/*
Fizz Buzz
*/
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string>ans;
        for(int i=1;i<=n;i++){
            if(i%3==0&&i%5==0) ans.push_back("FizzBuzz");
            else if(i%3==0) ans.push_back("Fizz");
            else if(i%5==0) ans.push_back("Buzz");
            else ans.push_back(to_string(i));            
        }
        return ans;
    }
};
```

