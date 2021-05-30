```c++
/*
翻转一棵二叉树
解法：递归
*/
class Solution{
  public:
    TreeNode *invertTree(TreeNode *root){
        if(root==NULL) return NULL;
        TreeNode *t=root->left;
        root->left=root->right;
        root->right=t;
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

```c++
/*
反转链表
题意：给你单链表的头节点head，请你反转链表，并返回反转后的链表
*/
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        vector<int>res;
        ListNode *p=head;
        while(p){
            res.push_back(p->val);
            p=p->next;
        }
        reverse(res.begin(),res.end());
        int k=0;
        p=head;
        while(p){
            p->val=res[k++];
            p=p->next;
        }
        return head;
    }
};
```

