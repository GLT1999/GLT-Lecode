```c++
/*
每日温度
题意：请根据每日气温列表，重新生成一个列表。对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用0来代替。
解法：单调栈、暴力
IN：[73, 74, 75, 71, 69, 72, 76, 73]
OUT：[1, 1, 4, 2, 1, 1, 0, 0]
*/
class Solution{
    public:
    	vector<int>dailyTemperatures(vector<int>& T){
            stack<int>st;
            vector<int>ans(T.size());
            for(int i=0;i<T.size();i++){
                while(!st.empty()&&T[i]>T[st.top()]){
                    ans[st.top()]=i-st.top();
                    st.pop();
                }
               	st.push(i);
            }
            return ans;
        }
};
class Solution{
    public:
    	vector<int>dailyTemperatures(vector<int>& T){
            vector<int>ans(T.size());
            for(int i=0;i<T.size()-1;i++){
                for(int j=i+1;j<T.size();j++){
                    if(T[j]>T[i]){
                        ans[i]=j-i;
                        break;
                    }
                }
            }
            return ans;
        }
};
```

