```c++
/*
DP背包问题：
0/1背包：外循环nums,内循环target,target倒序且target>=nums[i];(每个元素最多选取一次)
完全背包：外循环nums,内循环target,target正序且target>=nums[i];(每个元素可以重复选择)
组合背包：外循环target,内循环nums,target倒序且target>=nums[i];(背包中的物品要考虑顺序)
(分组背包：三重循环：外循环背包bags,内部两层循环根据题目的要求转化为1,2,3三种背包类型的模板(不止一个背包))

最值问题: dp[i] = max/min(dp[i], dp[i-nums]+1)或dp[i] = max/min(dp[i], dp[i-num]+nums);
存在问题：dp[i]=dp[i]||dp[i-num];
组合问题：dp[i]+=dp[i-num];
----------------------------------------------------------------------------------------------------
/*
分割等和子集
题意：判断是否能将一个数组分割为两个子集,其和相等
解法：0-1背包存在问题
*/
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=accumulate(nums.begin(),nums.end(),0);
        if(sum&1==1) return false;
        int target=sum/2;
        vector<int>dp(target+1,0);
        dp[0]=1;
        for(auto x: nums){
            for(int i=target;i>=x;i--) dp[i]=dp[i]||dp[i-x];
        }
        return dp[target]!=0;
    }
};
-----------------------------------------------------------------------------------------------------
/*零钱兑换
题意：不同面额的硬币 coins 和一个总金额 amount，计算可以凑成总金额所需的最少的硬币个数
解法：完全背包最值问题
*/
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<long long>dp(amount+1,INT_MAX);
        dp[0]=0;
        for(auto &x:coins){
            for(int i=0;i<=amount;i++){
                if(i>=x) dp[i]=min(dp[i],dp[i-x]+1);
            }
        }
        return dp[amount]==INT_MAX?-1:dp[amount];
    }
};
/*
零钱兑换 II
题意：给定不同面额的硬币和一个总金额，写出函数来计算可以凑成总金额的硬币组合数，假设每一种面额的硬币有无限个
解法：完全背包组合问题
*/
class Solution{
  public:
    int change(int amount,vector<int>&coins){
        vector<int>dp(amount+1);
        dp[0]=1;
        for(auto &x:coins){
            for(int i=0;i<=amount;i++){
                if(i>=x) dp[i]+=dp[i-x];
            }
        }
        return dp[amount];
    }
};
/*
完全平方数
题意：给定正整数n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于n，你需要让组成和的完全平方数的个数最少
解法：完全背包最值问题
*/
class Solution {
public:
    int numSquares(int n) {
        vector<int>dp(n+1,INT_MAX);
        dp[0]=0;
        for(int i=1;i<=sqrt(n);i++){
            for(int j=0;j<=n;j++){
                if(j>=pow(i,2)) dp[j]=min(dp[j],dp[j-pow(i,2)]+1);
            }
        }
        return dp[n];
    }
};
-----------------------------------------------------------------------------------------------------
/*
组合总和 Ⅳ
题意：给你一个由 不同 整数组成的数组 nums ，和一个目标整数 target,请你从 nums 中找出并返回总和为 target 的元素组合的个数
解法：考虑顺序的组合问题
*/
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<long long >dp(target+1);
        dp[0]=1;
        sort(nums.begin(),nums.end());
        for(int i=1;i<=target;i++){
            for(int x:nums){
                if(x<=i) dp[i]+=dp[i-x];
                dp[i]%=INT_MAX;
            }
        }
        return dp[target];
    }
};
//超时DFS
void combine(vector<int>&nums,int target,int sum,int &res){
    if(sum>=target){
        if(sum==target) res++;
        return ;
    }
    for(int i=0;i<nums.size();i++) combine(nums,target,sum+nums[i],res);
}
```

