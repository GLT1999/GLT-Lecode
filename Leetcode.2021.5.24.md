```c++
/*
把二叉搜索树转换为累加树
题意：按右-根-左遍历累加
*/
class Solution{
    public:
    int sum=0;
    TreeNode *convertBST(TreeNode *root){
        DFS(root);
        return root;
    }
    void DFS(TreeNode *root){
        if(root){
            DFS(root->right);
            sum+=root->val;
            root->val=sum;
            DSF(root->left);
        }
    }
};
```

```c++
/*
目标和
题意：给你一个整数数组nums和一个整数target，等于target的不同表达式的数目
解法：DFS
*/
class Solution{
public:
  int findTargetSumWays(vector<int>& nums,int target){
      int res=0;
      DFS(nums,res,target,0,0);
      return res;
  }
  void DFS(vector<int>&nums,int &res,int target,int t,int index){
      if(index==nums.size()){
          if(t==target) res++;
      }
      else{
          DFS(nums,res,target,t+nums[index],index+1);
          DFS(nums,res,target,t-nums[index],index+1);
      }
  }
};
```

