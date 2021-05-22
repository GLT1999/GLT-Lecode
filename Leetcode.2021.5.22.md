```c++
/*
最短无序连续子数组
解法：排序+双指针
*/
class Solution{
    public:
    int findUnsortedSubarray(vector<int>& nums){
        vector<int>res(nums.begin(),nums.end());
        sort(res.begin(),res.end(),less<int>());
        int i=0,j=nums.size()-1;
        while(i<j){
            int flag=1;
            if(nums[i]==res[i]){i++,flag=0;}
            if(nums[j]==res[j]){j--,flag=0;}
            if(flag==1) break;
        }
        if(i>=j) return 0;
        return j-i+1;
    }
}
```

```c++
/*
合并二叉树
题意：合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点
*/
struct TreeNode{
    int val;
    TreeNode *left,*right;
    TreeNode():val(0),left(nullptr),right(nullptr){}
    TreeNode(int x):val(x),left(nullptr),right(nullptr){}
    TreeNode(int x,TreeNode *left,TreeNode *right):val(x),left(left),right(right){}
};
class Solution{
  public:
    TreeNode *mergeTrees(TreeNode *root1,TreeNode *root2){
        if(root1==NULL) return root2;
        if(root2==NULL) return root1;
        root1->val+=root2->val;
        root1->left=mergeTrees(root1->left,root2->left);
        root1->right=mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```

