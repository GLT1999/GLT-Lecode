```c++
/*
和为s的两个数字
解法：输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可
*/
```

```c++
//解法：hash+暴力
class Solution{
  public:
  vector<int>twoSum(vector<int>&nums,int target){
      map<int,int>mp;
      vector<int>ans;
      for(auto &x:nums){
          if(mp.count(target-x)){
              ans.push_back(x);
              ans.push_back(target-x);
              return ans;
          }
          mp[x]=x;
      }
      return ans;
  }  
};
```

```c++
//解法：双指针
class Solution{
  public:
  vector<int>twoSum(vector<int>&nums,int target){
      int l=0,r=nums.size()-1;
      vector<int>ans;
      while(l<r){
          if(nums[l]+nums[r]>target) r--;
          else if(nums[l]+nums[r]<target) l++;
          else{
              ans.push_back(nums[l]);
              ans.push_back(nums[r]);
              break;
          }
      }
      return ans;
  }  
};
```

```c++
/*
和为s的连续正数序列
题意：输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）
*/
```

```c++
//解法：暴力
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
		vector<vector<int>> ans;
         for(int i=1;i<target;i++){
             int sum=0;
             vector<int>res;
             for(int j=i;j<target;j++){
                 if(sum<target){
                     res.push_back(j);
                     sum+=j;
                 }
                 else if(sum==target){
                     ans.push_back(res);
                     break;
                 }
                 else if(sum>target) break;
             }
         }
        return ans;
    }
};
```

```c++
//解法：双指针
class Solution{
  public:
    vector<vector<int>> findContinuousSequence(int target){
     	vector<vector<int>>ans;
        int i=1,j=2,s=3;
        while(i<target){
            if(s==target){
                vector<int>res;
                for(int k=i;k<=j;k++) res.push_back(k);
                ans.push_back(res);
            }
            if(s<target){
                j++;
                s+=j;
            }
            else if(s>=target){
                s-=i;
                i++;
            }
        }
        return ans;
    }
};
```

