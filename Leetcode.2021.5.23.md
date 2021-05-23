```c++
/*
二叉树的直径
题意：任意两结点最大长度为树直径
解法：递归
*/
class Solution{
public:
    int diameterOfBinaryTree(TreeNode* root){
        if(root==NULL) return 0;
        return max(max(diameterOfBinaryTree(root->left),diameterOfBinaryTree(root->right)),
        deep(root->left)+deep(root->right));
    }
    int deep(TreeNode *root){
        if(root==NULL) return 0;
        return max(deep(root->left),deep(root->right))+1;
    }
};

/*
和为k的子数组
题意：和为k的连续的子数组的个数
*/
//暴力：超时
class Solution{
    public:
    int subarraysum(vector<int>nums,int k){
        int len=nums.size();
        int count=0;
        for(int left=0;left<len;left++){
            for(int right=left;right<len;right++){
                int sum=0;
                for(int i=left;i<=right;i++) sum+=nums[i];
                if(sum==k) count++;
            }
        }
        return count;
    }
}
//暴力+前缀：超时
class Solution{
    public:
    int subarraysum(vector<int>nums,int k){
        int len=nums.size();
        int count=0;
        vector<int>presum(nums.size()+1);
        presum[0]=0;
        for(int i=0;i<len;i++) presum[i+1]=presum[i]+nums[i];
        for(int left=0;left<len;left++){
            for(int right=left;right<len;right++){
                if(presum[right+1]-presum[left]==k) count++;
            }
        }
        return count;
    }
}
//哈希+前缀
class Solution{
    public:
    int subarraySum(vector<int>&nums,int k){
        unordered_map<int,int>mp;
        int sum=0;
        int ans=0;
        mp[0]=1;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
            if(mp.find(sum-k)!=mp.end()) ans+=mp[sum-k];
            mp[sum]++;
        }
        return ans;
    }
};
```

