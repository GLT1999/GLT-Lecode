```c++
/*
字符串解码
解法：双栈
*/
class Solution{
    public:
    string decodeString(string s){
        stack<int>nums;
        stack<string>st;
        string ans;
        int res=0;
        for(int i=0;i<s.size();i++){
            if(isdigit(s[i])) res=res*10+s[i]-'0';
            else if(s[i]=='['){
                nums.push(res);
                st.push(ans);
                ans.clear();
                res=0;
            }
            else if(isalpha(s[i])) ans+=s[i];
            else if(s[i]==']'){
                int k=nums.top();nums.pop();
                for(int j=0;j<k;j++) st.top()+=ans;
                ans=st.top();st.pop();
            }
        }
        return ans;
    }
};
```

```c++
/*
根据身高重建队列
解法：重载排序
*/
class Solution{
    public:
    struct cmp{
        bool operator()(vector<int>&a,vector<int>&b){
            if(a[0]==b[0]) return a[1]<b[1];
            return a[0]>b[0];
        }
    };
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people){
        sort(people.begin(),people.end(),cmp());
        vector<vector<int>> ans;
        for(int i=0;i<people.size();i++){
            if(people[i][1]>=ans.size()) ans.push_back(people[i]);
            else ans.insert(ans.begin()+people[i][1],people[i]);
        }
        return ans;
    }
};
```

