```C++
/*
环形链表 II
题意：给定一个链表，返回链表开始入环的第一个节点，如果链表无环，则返回 null
考察：快慢双指针
*/
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow=head,*fast=head;
        while(true){
            if(fast==NULL||fast->next==NULL) return NULL;
            slow=slow->next;
            fast=fast->next->next;
            if(fast==slow) break;
        }
        fast=head;
        while(slow!=fast){
            fast=fast->next;
            slow=slow->next;
        }
        return fast;
    }
};
```

```c++
/*
乘积最大子数组
题意：给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组
*/
class Solution{
    public:
    int masProduct(vector<int>& nums){
        int ans=nums[0],res=1;
        for(int i=0;i<nums.size();i++){
            res*=nums[i];
            ans=max(ans,res);
            if(nums[i]==0) res=1;
        }
        res=1;
        for(int i=nums.size()-1;i>=0;i--){
            res*=nums[i];
            ans=max(ans,res);
            if(nums[i]==0) res=1;
        }
        return ans;
    }
}
```

