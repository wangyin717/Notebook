# 代码随想录
### 150.逆波兰表达式 
🧀[LeetCode_Link](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)
```cpp
# include "iostream"
using namespace std;
#include <string>
#include <stack>
#include <vector>

 //逆波兰表达式  
int func(string s){
    stack<char> st;
    for(int i = 0; i < s.size(); i++){
        if (s[i] == '+'){
            int num1 = st.top();
            st.pop();
            int num2 = st.top();
            st.pop();
            st.push(num1 + num2);
        }
        else if (s[i] == '-'){
            int num1 = st.top();
            st.pop();
            int num2 = st.top();
            st.pop();
            st.push(num1 - num2);
        }
        else if (s[i] == '*'){
            int num1 = st.top();
            st.pop();
            int num2 = st.top();
            st.pop();
            st.push(num1 * num2);
        }
        else if (s[i] == '/'){
            int num1 = st.top();
            st.pop();
            int num2 = st.top();
            st.pop();
            st.push(num1 / num2);
        }
        else{
            st.push(int(s[i])-48);
        }
    }
    return st.top();
}

int main(){
    string s = "21+3*";
    int res = func(s);
    cout << res << endl;
    return 0;
}
```

### 239.滑动窗口最大值
🧀[LeetCode_Link](https://leetcode.cn/problems/sliding-window-maximum/)
```cpp
#include <deque>
#include <vector>
# include "iostream"
using namespace std;

// 滑动窗口


void pop(int val, deque<int> & que){
    if(!que.empty() && val == que.front()){
        que.pop_front();
    }
}

void push(int val, deque<int> & que){
    while (!que.empty() && val > que.back()){
        que.pop_back();
    }
    que.push_back(val);
}

int GetMaxValue(deque<int> & que){
    return que.front();
}

int main(){
    int k = 3;
    vector<int> res;
    deque<int> que;
    int num[] = {1,3,-1,-3,5,3,6,7};
    for(int i=0; i < k; i++){
        push(num[i], que);
    }
    res.push_back(GetMaxValue(que));
    for (int i = k; i < sizeof (num) / sizeof (num[0]); i++){
        pop(num[i-k], que);
        push(num[i], que);
        res.push_back(GetMaxValue(que));
    }

    return 0;

}
```










