```c++
/*
排序链表
题意：给你链表的头结点 head ，请将其按 升序 排列并返回 排序后的链表
*/
class Solution{	
  public:
    ListNode *sortList(ListNode *head){
        multiset<int>box;//红黑树
        ListNode *sign=head;
        while(sign) box.insert(sign->val),sign=sign->next;
        sign=head;
        for(auto &x:box){
            sign->val=x;
            sign=sign->next;
        }
        return head;
    }
};
class Solution{
    public:
    ListNode *sortList(ListNode *head){
        priority_queue<int,vector<int>,greater<int>>box;//堆排序
        auto sign=head;
        while(sign) box.push(sign->val),sign=sign->next;
        sign=head;
        while(sign){
            sign->val=box.top(),box.pop();
            sign=sign->next;
        }
        return head;
    }
};
class Solution{
  public:
    ListNode *sortList(ListNode *head){//快排
        vector<int>v;
        auto sign=head;
        while(sign) v.push_back(sign->val),sign=sign->next;
        quickSort(v,0,v.size()-1);
        sign=head;
        for(auto &x:v) sign->val=x,sign=sign->next;
        return head;
    }
  private:
    void quickSort(vector<int>&v,int l,int r){
        if(l>=r) return ;
        int res=patition(v,l,r);
        quickSort(v,l,res-1);
        quickSort(v,res+1,r);
    }
    int patition(vector<int>&v,int l,int r){
        for(int i=l;i<r;i++){
            if(v[i]<v[r]) swap(v[l++],v[i]);
        }
        swap(v[l],v[r]);
        return l;
    }
};
```

```c++
/*
相交链表
题意：编写一个程序，找到两个单链表相交的起始节点
*/
class Solution{
    public:
    ListNode *getIntersectionNode(ListNode *headA,ListNode *headB){
        int A=0,B=0;
        ListNode *ptrA=headA,*ptrB=headB;
        while(ptrA) ptrA=ptrA->next,A++;
        while(ptrB) ptrB=ptrB->next,B++;
        ptrA=headA;
        ptrB=headB;
        int res=abs(A-B);
        if(A>B){
            while(ptrA&&res--) ptrA=ptrA->next;
            while(ptrA){
                if(ptrA==ptrB) return ptrA;
                ptrA=ptrA->next;
                ptrB=ptrB->next;
            }
        }
        else{
            while(ptrB&&res--) ptrB=ptrB->next;
            while(ptrB){
                if(ptrB==ptrA) return ptrA;
                ptrA=ptrA->next;
                ptrB=ptrB->next;
            }
        }
        return NULL;
    }
};
```

