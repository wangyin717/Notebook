## 代码随想录
#### 150.逆波兰表达式
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
