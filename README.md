# 代码随想录
[150 逆波兰表达式](#150-逆波兰表达式)

[239 滑动窗口最大值](#239-滑动窗口最大值)

[347 前K个高频元素](#347-前K个高频元素)

[1047 删除相邻重复项](#1047-删除相邻重复项)

[二叉树前/中/后序遍历](#二叉树前中后序遍历)

[102 二叉树层序遍历](#102-二叉树层序遍历)

[226 翻转二叉树](#226-翻转二叉树)

[101 对称二叉树](#101-对称二叉树)

[104 二叉树最大深度](#104-二叉树最大深度)

[559 N叉树最大深度](#559-N叉树最大深度)

[111 二叉树的最小深度](#111-二叉树的最小深度)

[700 二叉搜索树中的搜索](#700-二叉搜索树中的搜索)

[98 验证二叉搜索树](#98-验证二叉搜索树)

[77 组合](#77-组合)

[216 组合总和3](#216-组合总和3)

[17 电话号码的字母组合](#17-电话号码的字母组合)

[131 分割回文串](#131-分割回文串)

[93 复原IP地址](#93-复原IP地址)

[78 子集](#78-子集)

[90 子集ii](#90-子集ii)

[46 全排列](#46-全排列)

[455 分发饼干](#455-分发饼干)

[53 最大子数组和](#53-最大子数组和)

[122 买卖股票的最佳时机ii](#122-买卖股票的最佳时机ii)

[55 跳跃游戏](#55-跳跃游戏)

[45 跳跃游戏ii](#45-跳跃游戏ii)

[1005 k次取反后最大化的数组和](#1005-k次取反后最大化的数组和)

[134 加油站](#134-加油站)

[135 分发糖果](#135-分发糖果)

[860 柠檬水找零](#860-柠檬水找零)

[406 根据身高重建队列](#406-根据身高重建队列)

[452 用最少数量的箭引爆气球](#452-用最少数量的箭引爆气球)

[435 用最少数量的箭引爆气球](#435-无重叠区间)

[763 划分字母区间](#763-划分字母区间)

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

### 104 二叉树最大深度
🧀[LeetCode_Link](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)
```cpp
# include "iostream"
using namespace std;
# include "deque"

struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;

    TreeNode() :  val(0), left(nullptr), right(nullptr){};
    TreeNode(int x) : val(x), left(nullptr), right(nullptr){};
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right){};
};

class Solution{
public:
    int maxDepth(TreeNode *root){
        // 最大深度就是二叉树的层数 层序遍历
        if(root == NULL) return 0;
        deque<TreeNode *> deq;
        deq.push_back(root);
        int depth = 0;
        while (!deq.empty()){
            int size = deq.size();
            depth++;
            for (int i = 0; i < size; ++i) {
                TreeNode *node = deq.front();
                deq.pop_front();
                if(node->left) deq.push_back(node->left);
                if(node->right) deq.push_back(node->right);
            }
        }
        return depth;
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
    int res = s.maxDepth(&k11);
    cout << "二叉树的最大深度为:" << res << endl;
    return 0;
}
```

### 559 N叉树最大深度
🧀[LeetCode_Link](https://leetcode.cn/problems/maximum-depth-of-n-ary-tree/)
```cpp
# include "iostream"
using namespace std;
# include "vector"
# include "deque"

class Node{
public:
    int val;
    vector<Node*> children;

    Node(){};

    Node(int _val){
        this->val = _val;
    }

    Node(int _val, vector<Node *> _children){
        this->val = _val;
        this->children = _children;
    }
};

class Solution{
public:
    int maxDepth(Node * root){
        if (root == NULL) return 0;
        deque<Node *> deq;
        deq.push_back(root);
        int depth = 0;
        while(!deq.empty()){
            depth++;
            int size = deq.size();
            for (int i = 0; i < size; ++i) {
                Node * node = deq.front();
                deq.pop_front();
                for (int j = 0; j < node->children.size(); ++j) {
                    if(node->children[j]) deq.push_back(node->children[j]);
                }
            }
        }
        return depth;
    }
};

int main(){
    // 从底层构建树
    vector<Node*> c3; // 孩子为空的
    Node t31 = Node(5, c3);
    Node t32 = Node(6, c3);
    vector<Node*> c2;
    c2.push_back(&t31);
    c2.push_back(&t32);
    Node t21 = Node(3, c2);
    Node t22 = Node(2, c3);
    Node t23 = Node(4, c3);
    vector<Node*> c1;
    c1.push_back(&t21);
    c1.push_back(&t22);
    c1.push_back(&t23);
    Node t11 = Node(1, c1);

    Solution s;
    int res = s.maxDepth(&t11);
    cout << "n叉树的最大深度为:" << res << endl;
    return 0;
}
```

### 111 二叉树的最小深度
🧀[LeetCode_Link](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)
```cpp
# include "iostream"
# include "vector"
# include "deque"
using namespace std;

// 构造二叉树
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
    int minDeepth(TreeNode *root){
        // 层序遍历
        if(root == NULL) return 0;
        deque<TreeNode *> deq;
        deq.push_back(root);
        int depth = 0;
        while(!deq.empty()){
            int size = deq.size();
            depth ++;
            for (int i = 0; i < size; ++i) {
                TreeNode *node = deq.front();
                deq.pop_front();
                if(node->left) deq.push_back(node->left);
                if(node->right) deq.push_back(node->right);
                if(!node->left && !node->right){
                    return depth;
                }
            }
        }
    } 
};

int main(){
    // 从底向上构建树
    struct TreeNode t31 = {15, NULL, NULL};
    struct TreeNode t32 = {7, NULL, NULL};
    struct TreeNode t22 = {20, &t31, &t32};
    struct TreeNode t21 = {9, NULL, NULL};
    struct TreeNode t11 = {3, &t21, &t22};

    Solution s;
    int res = s.minDeepth(&t11);
    cout << "二叉树的最小深度为:" << res << endl;
}
```

### 700 二叉搜索树中的搜索
🧀[LeetCode_Link](https://leetcode.cn/problems/search-in-a-binary-search-tree/)
```cpp
# include "iostream";
using namespace std;
# include "deque";
# include "vector"
# include "algorithm"

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
    TreeNode *searchBST(TreeNode *root, int _val){
        while(root != NULL){
            if(_val < root->val) root = root->left;
            else if(_val > root->val) root = root->right;
            else return root;
        }
        return NULL;
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

class myprint{
public:
    void operator()(int val){
        cout << val << "\t";
    }
};

int main(){
    struct TreeNode t31 = {1, NULL, NULL};
    struct TreeNode t32 = {3, NULL, NULL};
    struct TreeNode t21 = {2, &t31, &t32};
    struct TreeNode t22 = {7, NULL, NULL};
    struct TreeNode t11 = {4, &t21, &t22};

    Solution s;
    PrintTree p;
    TreeNode *res = s.searchBST(&t11, 2);
    vector<int> r = p.levelOrder(res);
    for_each(r.begin(), r.end(), myprint());
    return 0;
}
```

### 98 验证二叉搜索树
🧀[LeetCode_Link](https://leetcode.cn/problems/validate-binary-search-tree/)
```cpp
# include "iostream";
using namespace std;
# include "stack"

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
    bool isValidBST(TreeNode *root){
        // 二叉搜索树中序遍历的结果是有序的
        stack<TreeNode*> st;
        TreeNode* pre = NULL;

        if(root != NULL){
            st.push(root);
        }
        while(!st.empty()){
            TreeNode *node = st.top();
            if(node != NULL){
                st.pop();
                // 中序遍历 右中左
                if(node->right) st.push(node->right);
                st.push(node);
                st.push(NULL);
                if(node->left) st.push(node->left);
            } else{
                st.pop();
                node = st.top();
                st.pop();
                if(pre != NULL && pre->val > node->val) return false;
                pre = node;
            }

        }
        return true;

    }
};

int main(){
    struct TreeNode t31 = {3, NULL, NULL};
    struct TreeNode t32 = {6, NULL, NULL};
    struct TreeNode t21 = {1, NULL, NULL};
    struct TreeNode t22 = {4, &t31, &t32};
    struct TreeNode t11 = {5, &t21, &t22};


    struct TreeNode tt21 = {1, NULL, NULL};
    struct TreeNode tt22 = {3, NULL, NULL};
    struct TreeNode tt11 = {2, &tt21, &tt22};

    Solution s;
    bool res = s.isValidBST(&t11);
    cout << res << endl;
    return 0;
}
```

### 77 组合
🧀[LeetCode_Link](https://leetcode.cn/problems/combinations/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;


class Solution{
private:
    vector<vector<int>> res;
    vector<int> path;
    void backtracking(int n, int k, int startindex){
        if(path.size() == k){
            res.push_back(path);
            return;
        }
        for (int i = startindex; i <= n; ++i) {
            path.push_back(i);
            backtracking(n, k, i+1);
            path.pop_back();
        }

    }
public:
    vector<vector<int>> combine(int n, int k){
        backtracking(n, k, 1);
        return res;
    }
};



int main(){
    Solution s;
    vector<vector<int>> res = s.combine(4, 2);
    for(vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++){
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << " ";
        }
        cout << endl;
    }
    return 0;
}
```

### 216 组合总和3
🧀[LeetCode_Link](https://leetcode.cn/problems/combination-sum-iii/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

class Solution{
private:
    vector<int> path;
    vector<vector<int>> res;
    void backtracking(int targetnum, int k, int sum, int startindex){
        if(path.size() == k){
            if(sum == targetnum) res.push_back(path);
            return;
        }

        for (int i = startindex; i <= 9; ++i) {
            path.push_back(i);
            sum += i;
            backtracking(targetnum, k, sum, i+1);
            path.pop_back();
            sum -= i;
        }
    }
public:
    vector<vector<int>> combinationSum3(int k, int n){
        backtracking(n, k, 0, 1);
        return res;
    }
};

int main(){
    Solution s;
    vector<vector<int>> res = s.combinationSum3(3, 9);
    for(vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++){
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << " ";
        }
        cout << endl;
    }
    return 0;
}
```

### 17 电话号码的字母组合
🧀[LeetCode_Link](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

const string letterMap[10] = {
        "", // 0
        "", // 1
        "abc", // 2
        "def", // 3
        "ghi", // 4
        "jkl", // 5
        "mno", // 6
        "pqrs", // 7
        "tuv", // 8
        "wxyz", // 9
};

class Solution{
private:
    vector<string> res;
    string s;
    void backtracking(string &digits, int index){
        if(index == digits.size()){
            res.push_back(s);
            return;
        }
        int digit = digits[index] - '0';
        string letters = letterMap[digit];
        for (int i = 0; i < letters.size(); ++i) {
            s.push_back(letters[i]);
            backtracking(digits, index + 1);
            s.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits){
        if (digits.size() == 0) {
            return res;
        }
        backtracking(digits, 0);
        return res;
    }
};

class myprint{
public:
    void operator()(string val){
        cout << val << "\t";
    }
};

int main(){
    Solution s;
    vector<string> res = s.letterCombinations("23");
    for_each(res.begin(), res.end(), myprint());
    return 0;
}
```

### 131 分割回文串
🧀[LeetCode_Link](https://leetcode.cn/problems/palindrome-partitioning/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

bool isPalindrome(const string &s, int start, int end){
    for (int i = start, j = end; i < j; ++i, --j) {
        if(s[i] != s[j]) return false;
    }
    return true;
}


class Solution{
private:
    vector<string> path;
    vector<vector<string>> res;
    void backtracking(const string &s, int startindex){
        if(startindex >= s.size()){
            res.push_back(path);
            return;
        }
        for (int i = startindex; i < s.size(); ++i) {
            if(isPalindrome(s, startindex, i)){
                path.push_back(s.substr(startindex, i-startindex+1));
            } else continue;
            backtracking(s, i+1);
            path.pop_back();
        }
    }
public:
    vector<vector<string>> partition(string s){
        backtracking(s, 0);
        return res;
    }
};

int main(){
    Solution s;
    string str = "aab";
    vector<vector<string>> res = s.partition(str);
    for(vector<vector<string>>::iterator it = res.begin(); it != res.end(); it++){
        for (vector<string>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << "\t";
        }
        cout << endl;
    }
    return 0;
}
```

### 93 复原IP地址
🧀[LeetCode_Link](https://leetcode.cn/problems/restore-ip-addresses/)
```cpp
# include "iostream"
# include "vector"
# include "string"
# include "algorithm"
using namespace std;

class Solution{
private:
    vector<string> res;
    void backtracking(string &s, int startindex, int pointnum){
        if(pointnum == 3){
            if(isValid(s, startindex, s.size()-1)){
                res.push_back(s);
            }
            return;
        }


        for (int i = startindex; i < s.size(); ++i) {
            if(isValid(s, startindex, i)){
                s.insert(s.begin() + i + 1, '.');
                pointnum ++;
                backtracking(s, i+2, pointnum);
                pointnum --;
                s.erase(s.begin() + i + 1);
            }
        }
    }

    bool isValid(const string &s, int start, int end){
        if(start > end){
            return false;
        }
        if(s[start] == 0 && start != end){
            return false;
        }
        int num = 0;
        for (int i = start; i <= end ; ++i) {
            if(s[i] > '9' || s[i] < '0'){
                return false;
            }
            num = num * 10 + (s[i] - '0');
            if (num > 255){
                return false;
            }
        }
        return true;
    }
public:
    vector<string> restoreIpAddresses(string s){
        backtracking(s, 0, 0);
        return res;
    }

};

class myprint{
public:
    void operator()(string val){
        cout << val << "\t";
    }
};

int main(){
    Solution s;
    string str = "25525511135";
    vector<string> res = s.restoreIpAddresses(str);
    for_each(res.begin(), res.end(), myprint());
    return 0;
}
```

### 78 子集
🧀[LeetCode_Link](https://leetcode.cn/problems/subsets/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
private:
    vector<vector<int>> res;
    vector<int> path;
    void backtracking(vector<int>& nums, int startIndex){
        res.push_back(path);

        for (int i = startIndex; i < nums.size(); ++i) {
            path.push_back(nums[i]);
            backtracking(nums, i+1);
            path.pop_back();
        }
    }
public:
    vector<vector<int>> subsets(vector<int>& nums){
        backtracking(nums, 0);
        return res;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(1);
    nums.push_back(2);
    nums.push_back(3);

    Solution s;
    vector<vector<int>> res = s.subsets(nums);
    for (vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++) {
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << "\t";
        }
        cout << endl;
    }
    return 0;
}
```

### 90 子集ii
🧀[LeetCode_Link](https://leetcode.cn/problems/subsets-ii/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

class Solution{
private:
    vector<int> path;
    vector<vector<int>> res;
    void backtracking(vector<int> &nums, int startindex, vector<bool> used){
        res.push_back(path);
        for (int i = startindex; i < nums.size(); ++i) {
            if(i > 0 && nums[i] == nums[i-1] && used[i-1] == false){
                continue;
            }
            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, i+1, used);
            used[i] = false;
            path.pop_back();

        }

    }
public:
    vector<vector<int>> subsetsWithDup(vector<int> &nums){
        vector<bool> used(nums.size(), false);
        sort(nums.begin(), nums.end());
        backtracking(nums, 0, used);
        return res;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(1);
    nums.push_back(2);
    nums.push_back(2);
    Solution s;
    vector<vector<int>> res = s.subsetsWithDup(nums);
    for (vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++) {
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << "\t";
        }
        cout << endl;
    }
    return 0;
}
```

### 46 全排列
🧀[LeetCode_Link](https://leetcode.cn/problems/permutations/)
```cpp
# include "iostream"
# include "vector"
using namespace std;
# include "algorithm"

class Solution{
private:
    vector<int> path;
    vector<vector<int>> res;
    void backtracking(vector<int>& nums, vector<bool> used){
        if(path.size() == nums.size()){
            res.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); ++i) {
            if(used[i] == true) continue;
            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, used);
            // 回溯
            path.pop_back();
            used[i] = false;
        }

    }\
 public:
    vector<vector<int>> permute(vector<int>& nums){
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);
        return res;
    }
};


int main(){
    vector<int> nums;
    nums.push_back(1);
    nums.push_back(2);
    nums.push_back(3);
    Solution s;
    vector<vector<int>> res = s.permute(nums);
    for (vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++) {
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << "\t";
        }
        cout << endl;
    }
    return 0;
}
```

### 455 分发饼干
🧀[LeetCode_Link](https://leetcode.cn/problems/assign-cookies/)
```cpp
# include "iostream"
# include "vector"
#include "algorithm"
using namespace std;

class Solution{
public:
    int findContentChildren(vector<int>& g, vector<int>& s ){
        int res = 0;
        int index = s.size() - 1;
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        for(int i = g.size(); i >= 0; i--){
            while(index > 0 && s[index] >= g[i]){
                res++;
                index--;
            }
        }
        return res;
    }
};

int main(){
    vector<int> g;
    g.push_back(1);
    g.push_back(2);
    g.push_back(3);

    vector<int> s;
    s.push_back(1);
    s.push_back(1);

    Solution sol;
    int res = sol.findContentChildren(g, s);
    cout << res << endl;
    return 0;
}
```

### 53 最大子数组和
🧀[LeetCode_Link](https://leetcode.cn/problems/maximum-subarray/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
public:
    int maxSubArray(vector<int>& nums){
        int res = INT32_MIN;
        int count = 0;
        for (int i = 0; i < nums.size(); ++i) {
            count += nums[i];
            if (count > res) res = count;
            if (count < 0) count = 0;
        }
        return res;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(-2);
    nums.push_back(1);
    nums.push_back(-3);
    nums.push_back(4);
    nums.push_back(-1);
    nums.push_back(2);
    nums.push_back(1);
    nums.push_back(-5);
    nums.push_back(4);
    Solution s;
    int res = s.maxSubArray(nums);
    cout << res << endl;
    return 0;
}
```

### 122 买卖股票的最佳时机ii
🧀[LeetCode_Link](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
public:
    int maxProfit(vector<int> prices){
        int res = 0;
        for (int i = 1; i < prices.size(); ++i) {
            res += max(prices[i] - prices[i-1], 0);
        }
        return res;
    }
};

int main(){
    vector<int> prices;
    prices.push_back(7);
    prices.push_back(1);
    prices.push_back(5);
    prices.push_back(10);
    prices.push_back(3);
    prices.push_back(6);
    prices.push_back(4);
    Solution s;
    int res = s.maxProfit(prices);
    cout << res << endl;
    return 0;
}
```

### 55 跳跃游戏
🧀[LeetCode_Link](https://leetcode.cn/problems/jump-game/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
public:
    bool canJump(vector<int>& nums){
        if(nums.size() == 1) return true;
        int cover = 0;
        for (int i = 0; i <= cover; ++i) {
            cover = max(i+nums[i], 0);
            if(cover + 1 >= nums.size()) return true;
        }
        return false;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(2);
    nums.push_back(3);
    nums.push_back(1);
    nums.push_back(1);
    nums.push_back(4);

    Solution s;
    bool res = s.canJump(nums);
    if(res == 1){
        cout << "能跳出" << endl;
    } else{
        cout << "不能跳出" << endl;
    }
    return 0;
}
```

### 45 跳跃游戏ii
🧀[LeetCode_Link](https://leetcode.cn/problems/jump-game/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
public:
    int jump(vector<int> nums){
        if(nums.size() == 0 ) return 0;
        int curDistance = 0;
        int nextDistance = 0;
        int res = 0;
        for (int i = 0; i < nums.size(); ++i) {
            nextDistance = max(nums[i] + 1, nextDistance);
            if(curDistance == i){
                if (curDistance < nums.size() - 1){
                    res++;
                    curDistance = nextDistance;
                    if(nextDistance + 1 >= nums.size()) break;
                }else{
                    break;
                }
            }
        }
        return res;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(2);
    nums.push_back(3);
    nums.push_back(1);
    nums.push_back(1);
    nums.push_back(4);

    Solution s;
    int res = s.jump(nums);
    cout << res ;
    return 0;
}
```

### 1005 k次取反后最大化的数组和
🧀[LeetCode_Link](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)
```cpp
# include "iostream"
# include "algorithm"
#include <numeric>
using namespace std;

bool cmp(int a, int b){
    return abs(a) > abs(b);  // 按照绝对值 从大到小排序
}

class Solution{
public:
    int largestSumAfterKNegations(vector<int>& nums, int k){
        sort(nums.begin(), nums.end(), cmp);
        for (int i = 0; i < nums.size(); ++i) {
            if(nums[i] < 0 && k > 0){
                nums[i] = -nums[i];
                k--;
            }
        }
        if(k > 0){          // 如果k还大于0 只需要反复转变数值最小的元素
            nums[nums.size()-1] = -nums[nums.size()-1];
        }


        int res = 0;
        res = accumulate(nums.begin(), nums.end(), 0); // 第三个参数表示累加的初值
        return res;
    }
};

int main(){
    vector<int> nums;
    nums.push_back(3);
    nums.push_back(-1);
    nums.push_back(0);
    nums.push_back(2);
    int k = 3;
    Solution s;
    int res = s.largestSumAfterKNegations(nums, k);
    cout << res;
    return 0;
}
```

### 134 加油站
🧀[LeetCode_Link](https://leetcode.cn/problems/gas-station/)
```cpp
# include "iostream"
# include "algorithm"
#include <numeric>
using namespace std;

class Solution{
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost){
        int curSum = 0;
        int totalSum = 0;
        int start = 0;
        for (int i = 0; i < gas.size(); ++i) {
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if(curSum < 0){
                start = i + 1;
                curSum = 0;
            }
        }
        if (totalSum < 0) return -1;
        return start;
    }
};

int main(){
    vector<int> gas;
    vector<int> cost;
    gas.push_back(1);
    gas.push_back(2);
    gas.push_back(3);
    gas.push_back(4);
    gas.push_back(5);

    cost.push_back(3);
    cost.push_back(4);
    cost.push_back(5);
    cost.push_back(1);
    cost.push_back(2);

    Solution s;
    int index = s.canCompleteCircuit(gas, cost);
    cout << index ;
    return 0;
}
```

### 135 分发糖果
🧀[LeetCode_Link](https://leetcode.cn/problems/candy/)
```cpp
# include "iostream"
# include "algorithm"
#include <numeric>
# include "numeric"
using namespace std;

class Solution{
public:
    int candy(vector<int>& ratings){
        vector<int> candyVec(ratings.size(), 1);
        for (int i = 1; i < ratings.size(); ++i) {
            if(ratings[i] > ratings[i-1]){
                candyVec[i] = candyVec[i-1] + 1;
            }
        }
        for (int j = ratings.size() - 2; j >= 0; j--) {
            if (ratings[j] > ratings[j+1]){
                candyVec[j] = max(candyVec[j], candyVec[j+1] + 1);
            }
        }
        int res = 0;
        res = accumulate(candyVec.begin(), candyVec.end(), 0);
        return res;
    }
};

int main(){
    vector<int> ratings;
    ratings.push_back(1);
    ratings.push_back(0);
    ratings.push_back(2);

    Solution s;
    int res = s.candy(ratings);
    cout << res;
    return 0;
}
```

### 860 柠檬水找零
🧀[LeetCode_Link](https://leetcode.cn/problems/candy/)
```cpp
# include "iostream"
# include "vector"
using namespace std;

class Solution{
public:
    bool lemonadeChange(vector<int>& bills){
        int five = 0;
        int ten = 0;
        int tw = 0;
        for (int i = 0; i < bills.size(); ++i) {
            if(bills[i] == 5){
                five++;
            }
            if (bills[i] == 10){
                if (five <= 0) return false;
                five--;
                ten++;
            }
            if(bills[i] == 20){
                if (five > 0 && ten > 0){
                    five--;
                    ten--;
                }
                else if(five >= 0){
                    five -= 3;
                }
                else return false;
            }

        }
        return true;
    }
};

int main(){
    vector<int> bills;
    bills.push_back(5);
    bills.push_back(5);
    bills.push_back(5);
    bills.push_back(10);
    bills.push_back(20);

    Solution s;
    bool res = s.lemonadeChange(bills);
    if(res == 1){
        cout << "能找开" << endl;
    } else cout << "找不开";
    return 0;
}
```

### 406 根据身高重建队列
🧀[LeetCode_Link](https://leetcode.cn/problems/queue-reconstruction-by-height/)
```cpp
# include "iostream"
# include "vector"
# include "deque"
# include "algorithm"
# include "list"
using namespace std;

class Solution{

public:
    static bool cmp(const vector<int>& a, const vector<int>& b){
        if(a[0] == b[0]) return a[1] < b[1];
        return a[0] > b[0];
    }
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people){
        sort(people.begin(), people.end(), cmp);
        vector<vector<int>> que;
        for (int i = 0; i < people.size(); ++i) {
            int position = people[i][1];
            que.insert(que.begin() + position, people[i]);
        }
        return que;
    }
    // 使用链表
    vector<vector<int>> reconstructQueue_List(vector<vector<int>>& people) {
        sort (people.begin(), people.end(), cmp);
        list<vector<int>> que; // list底层是链表实现，插入效率比vector高的多
        for (int i = 0; i < people.size(); i++) {
            int position = people[i][1]; // 插入到下标为position的位置
            list<vector<int>>::iterator it = que.begin();
            while (position--) { // 寻找在插入位置
                it++;
            }
            que.insert(it, people[i]);
        }
        return vector<vector<int>>(que.begin(), que.end());
    }
};

int main(){
    vector<vector<int>> people;
    vector<int> p1;
    p1.push_back(7);
    p1.push_back(0);
    people.push_back(p1);
    vector<int> p2;
    p2.push_back(4);
    p2.push_back(4);
    people.push_back(p2);
    vector<int> p3;
    p3.push_back(7);
    p3.push_back(1);
    people.push_back(p3);
    vector<int> p4;
    p4.push_back(5);
    p4.push_back(0);
    people.push_back(p4);
    vector<int> p5;
    p5.push_back(6);
    p5.push_back(1);
    people.push_back(p5);
    vector<int> p6;
    p6.push_back(5);
    p6.push_back(2);
    people.push_back(p6);

    Solution s;
    vector<vector<int>> res = s.reconstructQueue_List(people);
    for (vector<vector<int>>::iterator it = res.begin(); it != res.end(); it++) {
        for (vector<int>::iterator itt = it->begin(); itt != it->end(); itt++) {
            cout << (*itt) << " ";
        }
        cout << " ";
    }
    return 0;
}
```

### 452 用最少数量的箭引爆气球
🧀[LeetCode_Link](https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

class Solution{
private:
    static bool cmp(vector<int>& a, vector<int>& b){
        return a[0] < b[0];
    }
public:
    int findMinArrowShots(vector<vector<int>>& points){
        sort(points.begin(), points.end(), cmp);
        int res = 1;
        if(points.size() == 0) return 0;
        for (int i = 1; i < points.size(); ++i) {
            if(points[i][0] > points[i-1][1]) res++;
            else{
                points[i][1] = min(points[i-1][1], points[i][1]);
            }
        }
        return res;
    }
};

int main(){
    vector<vector<int>> points;
    vector<int> p1;
    p1.push_back(10);
    p1.push_back(16);
    points.push_back(p1);
    vector<int> p2;
    p2.push_back(2);
    p2.push_back(8);
    points.push_back(p2);
    vector<int> p3;
    p3.push_back(1);
    p3.push_back(6);
    points.push_back(p3);
    vector<int> p4;
    p4.push_back(7);
    p4.push_back(12);
    points.push_back(p4);

    Solution s;
    int res = s.findMinArrowShots(points);
    cout << res;
    return 0;
}
```

### 435 无重叠区间
🧀[LeetCode_Link](https://leetcode.cn/problems/non-overlapping-intervals/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

class Solution{
public:
    static bool cmp(vector<int>& a, vector<int>& b){
        return a[0] < b[0];
    }

    int eraseOverlapIntervals(vector<vector<int>> intervals){
        sort(intervals.begin(), intervals.end(), cmp);
        int end = intervals[0][1];
        int count = 0;
        for (int i = 1; i < intervals.size(); ++i) {
            if(intervals[i][1] > end) end = intervals[i][1];
            else{
                // 重叠情况
                count++;
                end = min(end, intervals[i][1]);
            }
        }
        return count;
    }
};

int main(){
    vector<vector<int>> points;
    vector<int> p1;
    p1.push_back(1);
    p1.push_back(2);
    points.push_back(p1);
    vector<int> p2;
    p2.push_back(2);
    p2.push_back(3);
    points.push_back(p2);
    vector<int> p3;
    p3.push_back(3);
    p3.push_back(4);
    points.push_back(p3);
    vector<int> p4;
    p4.push_back(1);
    p4.push_back(3);
    points.push_back(p4);

    Solution s;
    int res =  s.eraseOverlapIntervals(points);
    cout << res;
    return 0;
}
```

### 763 划分字母区间
🧀[LeetCode_Link](https://leetcode.cn/problems/partition-labels/)
```cpp
# include "iostream"
# include "vector"
# include "algorithm"
using namespace std;

class Solution{
public:
    vector<int> partitionLabels(string s){
        int hash[27] = {0};
        for (int i = 0 ; i < s.size(); ++i) {
            hash[s[i] - 'a'] = i;
        }
        vector<int> res;
        int left = 0;
        int right = 0;
        for (int i = 0; i < s.size(); ++i) {
            right = max(hash[s[i] - 'a'], right);
            if(right == i){
                res.push_back(right - left + 1);
                left = i + 1;
            }
        }
        return res;
    }
};

void myprint(int val){
    cout << val <<endl;
}


int main(){
    string str = "ababcbacadefegdehijhklij";
    Solution s;
    vector<int> res = s.partitionLabels(str);
    for_each(res.begin(), res.end(), myprint);
    return 0;
}
```











