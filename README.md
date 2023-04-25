# 代码随想录
[150 逆波兰表达式](#150-逆波兰表达式)

[239 滑动窗口最大值](#239-滑动窗口最大值)

[347 前K个高频元素](#347-前K个高频元素)

[1047 删除相邻重复项](#1047-删除相邻重复项)

[二叉树前/中/后序遍历](#二叉树前中后序遍历)

[102 二叉树层序遍历](#102-二叉树层序遍历)

[226 翻转二叉树](#226-翻转二叉树)

[101 对称二叉树](#101-对称二叉树)

### 150 逆波兰表达式
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

### 239 滑动窗口最大值
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

### 347 前K个高频元素
🧀[LeetCode_Link](https://leetcode.cn/problems/top-k-frequent-elements/)
```cpp
#include <unordered_map>
#include <queue>
# include "iostream"
using namespace std;

vector<int> test01(int *num, int len, int k){
    unordered_map<int, int> map;
    priority_queue<pair<int, int>> pri_que;
    for (int i = 0; i < len; i++){
        map[num[i]] ++;
    }
    int it;
    for(unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++){
        pri_que.push(*it);
        if (pri_que.size() > k){
            pri_que.pop();
        }
    }
    vector<int> res(k);
    for (int i = k-1; i >=0 ; i--){
        res[i] = pri_que.top().first;
        pri_que.pop();
    }
    return res;

}

int main(){
    int nums[] = {1,1,1,2,2,3};
    int k = 2;
    int len = (sizeof (nums) / sizeof (nums[0]));
    vector<int> res = test01(nums, len, k);
    cout << "这里" << endl;
    return 0;
}
```

### 1047 删除相邻重复项
🧀[LeetCode_Link](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)
```cpp
# include "iostream"
using namespace std;
 // 删除相邻重复项
string func(string s){
    string result;
    for (int i = 0; i < s.size(); i++){
        if(result.empty() || s[i] != result.back())
        {
            result.push_back(s[i]);
        }
        else
        {
            result.pop_back();
        }
    }
    return result;
}

int main(){
    string s = "abbaca";
    string res = func(s);
    cout << res << endl;
    return 0;
}
```

### 二叉树前中后序遍历
🧀[LeetCode_Link(前)](https://leetcode.cn/problems/binary-tree-preorder-traversal/)
🧀[LeetCode_Link(中)](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
🧀[LeetCode_Link(后)](https://leetcode.cn/problems/binary-tree-postorder-traversal/)
```cpp
# include "iostream"
using namespace std;
# include "vector"
# include "stack"

struct TreeNode {
     int val;
     TreeNode *left;
     TreeNode *right;
     TreeNode() : val(0), left(nullptr), right(nullptr) {}
     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution_front {
public:
    // 返回值为vector的函数
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> st;
        if (root != NULL) st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();
            if (node != NULL) {
                st.pop();
                if (node->right) st.push(node->right);  // 右
                if (node->left) st.push(node->left);    // 左
                st.push(node);                          // 中
                st.push(NULL);
            } else {
                st.pop();
                node = st.top();
                st.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};

class Solution_middle {
public:
    vector<int> preorderTraversal(TreeNode *root){
        vector<int> result;
        stack<TreeNode*> st;
        if(root != NULL){
            st.push(root);
        }
        while(!st.empty()){
            TreeNode *node = st.top();
            if(node != NULL){
                st.pop();
                // 右
                if(node->right){
                    st.push(node->right);
                }
                // 中
                st.push(node);
                st.push(NULL);
                // 左
                if(node->left){
                    st.push(node->left);
                }
            } else{
                st.pop();
                node = st.top();
                st.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};

class Solution_back{
public:
    vector<int> preorderTraversal(TreeNode *root){
        vector<int> result;
        stack<TreeNode *> st;
        if (root != NULL){
            st.push(root);
        }
        while (!st.empty()){
            TreeNode *node = st.top();
            if(node != NULL){
                st.pop();
                // 中
                st.push(node);
                st.push(NULL);
                // 右
                if (node->right){
                    st.push(node->right);
                }
                // 左
                if (node->left){
                    st.push(node->left);
                }
            } else{
                st.pop();
                node = st.top();
                st.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }

};

int main(){
    // 第一个树 从底向上构建二叉树
    struct TreeNode t2 = {3, NULL, NULL};
    struct TreeNode t1 = {2, &t2, NULL};
    struct TreeNode t0 = {1, NULL, &t1};

    // 第二个树
    struct TreeNode s1 = {2, NULL, NULL};
    struct TreeNode s0 = {1, NULL, &s1};

    Solution_back s;
    vector<int> res = s.preorderTraversal(&t0);

    for(vector<int>::iterator it = res.begin(); it != res.end(); it++){
        cout << (*it) << "\t";
    }
    return 0;
}
```

### 102 二叉树层序遍历
🧀[LeetCode_Link](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

![Image 1](https://github.com/wangyin717/Notebook_Algorithm/blob/master/p1.png)
```cpp
# include "iostream"
using namespace std;
# include "vector"
# include "queue"


struct TreeNode {
     int val;
     TreeNode *left;
     TreeNode *right;
     // 结构体构造函数 初始化三个值
     // 重载构造函数
     TreeNode() : val(0), left(nullptr), right(nullptr) {}
     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode *root){
        // 层序遍历
        // 准备一个队列存放二叉树
        deque<TreeNode*> deq;
        if(root != NULL) deq.push_back(root);
        // 准备一个vector容器存放结果
        vector<vector<int>> result;
        while(!deq.empty()){
            int size = deq.size();
            vector<int> vec;
            for(int i = 0; i < size; i++){
                TreeNode *node = deq.front();
                deq.pop_front();
                if (node->left) deq.push_back(node->left);
                if (node->right) deq.push_back(node->right);
                vec.push_back(node->val);
            }
            result.push_back(vec);
        }
        return result;
    }
};

int main(){
        // 第一个树
    struct TreeNode t2 = {3, NULL, NULL};
    struct TreeNode t1 = {2, &t2, NULL};
    struct TreeNode t0 = {1, NULL, &t1};

    // 第二个树
    struct TreeNode s1 = {2, NULL, NULL};
    struct TreeNode s0 = {1, NULL, &s1};

    // 第三个树
    struct TreeNode k31 = {1, NULL, NULL};
    struct TreeNode k32 = {3, NULL, NULL};
    struct TreeNode k33 = {5, NULL, NULL};
    struct TreeNode k34 = {8, NULL, NULL};

    struct TreeNode k21 = {4, &k31, &k32};
    struct TreeNode k22 = {7, &k33, &k34};

    struct TreeNode k11 = {6, &k21, &k22};

    Solution s;
    vector<vector<int>> res = s.levelOrder(&k11);

    for(vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++){
        for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++) {
            cout << *vit << "\t";
        }
        cout << endl;
    }
    return 0;
}
```

### 226 翻转二叉树
🧀[LeetCode_Link](https://leetcode.cn/problems/invert-binary-tree/)
![Image 2](https://github.com/wangyin717/Notebook_Algorithm/blob/master/p2.png)
```cpp
# include "iostream";
using namespace std;
# include "vector";
# include "stack";

struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr){};
    TreeNode(int x) : val(x), left(nullptr), right(nullptr){};
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right){};
};

class Solution{
public:
    TreeNode* invertTree(TreeNode* root) {
        // 在前序遍历中 交换左右孩子
        vector<int> res;
        stack<TreeNode*> st;
        if (root != NULL){
            st.push(root);
        }
        while(!st.empty()){
            TreeNode* node  = st.top();
            if(node != NULL){
                st.pop();
                // 右
                if(node->right) st.push(node->right);
                // 左
                if(node->left) st.push(node->left);
                // 中
                st.push(node);
                st.push(NULL);
            } else{
                st.pop();
                node = st.top();
                swap(node->right, node->left);
                st.pop();
            }
        }
        return root;
    }
};

class PrintTree {
public:
    vector<int> levelOrder(TreeNode *root){
        // 层序遍历
        // 准备一个队列存放二叉树
        deque<TreeNode*> deq;
        if(root != NULL) deq.push_back(root);
        // 准备一个vector容器存放结果
        vector<int> result;
        while(!deq.empty()){
            int size = deq.size();
            for(int i = 0; i < size; i++){
                TreeNode *node = deq.front();
                deq.pop_front();
                if (node->left) deq.push_back(node->left);
                if (node->right) deq.push_back(node->right);
                result.push_back(node->val);
            }
        }
        return result;
    }
};

int main(){
    // 第三个树
    struct TreeNode k31 = {1, NULL, NULL};
    struct TreeNode k32 = {3, NULL, NULL};
    struct TreeNode k33 = {5, NULL, NULL};
    struct TreeNode k34 = {8, NULL, NULL};

    struct TreeNode k21 = {4, &k31, &k32};
    struct TreeNode k22 = {7, &k33, &k34};

    struct TreeNode k11 = {6, &k21, &k22};

    // 翻转前
    cout << "翻转前:" << endl;
    PrintTree p_before;
    vector<int> r_before = p_before.levelOrder(&k11);
    for(vector<int>::iterator it = r_before.begin(); it != r_before.end(); it++) {
        cout << *it << "\t";
    }
    cout << endl;
    // 翻转后
    cout << "翻转前:" << endl;
    Solution s;
    TreeNode* res = s.invertTree(&k11);
    PrintTree p_after;
    vector<int> r_after = p_after.levelOrder(res);

    for(vector<int>::iterator it = r_after.begin(); it != r_after.end(); it++) {
            cout << *it << "\t";
    }
    return 0;

}
```

### 101 对称二叉树
🧀[LeetCode_Link](https://leetcode.cn/problems/symmetric-tree/)
![Image 3](https://github.com/wangyin717/Notebook_Algorithm/blob/master/p3.png)
```cpp
# include "iostream"
using namespace std;
# include "deque";

struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr){};
    TreeNode(int x) : val(x), left(nullptr), right(nullptr){};
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right){};
};

class Solution{
public:
    bool isSymmetric(TreeNode *root){
        if (root == NULL) return true;
        // 创建队列
        deque<TreeNode*> deq;
        // 将根节点的左右孩子放入队列
        deq.push_back(root->left);
        deq.push_back(root->right);
        while (!deq.empty()){
            TreeNode *leftnode = deq.front();
            deq.pop_front();
            TreeNode *rightnode = deq.front();
            deq.pop_front();
            // 如果左右节点为空 继续循环
            if(!leftnode && !rightnode){
                continue;
            }
            // 如果左右一个不为空 或 左右不为空 但值不同 -> 不对称
            if(!leftnode || !rightnode || (leftnode->val != rightnode->val)){
                return false;
            }
            deq.push_back(leftnode->left);
            deq.push_back(rightnode->right);
            deq.push_back(leftnode->right);
            deq.push_back(rightnode->left);

        }
        return true;

    }
};


int main(){
    // 第三个树
    struct TreeNode k31 = {3, NULL, NULL};
    struct TreeNode k32 = {4, NULL, NULL};
    struct TreeNode k33 = {4, NULL, NULL};
    struct TreeNode k34 = {3, NULL, NULL};

    struct TreeNode k21 = {2, &k31, &k32};
    struct TreeNode k22 = {2, &k33, &k34};

    struct TreeNode k11 = {1, &k21, &k22};
    Solution s;
    bool issym = s.isSymmetric(&k11);
    if(issym == 1){
        cout << "对称" << endl;
    } else{
        cout << "不对称" << endl;
    }
    return 0;
}
```














