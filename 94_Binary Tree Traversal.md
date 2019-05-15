>https://leetcode.com/problems/binary-tree-inorder-traversal/

**EXPRESSION**

Given a binary tree, return the inorder traversal of its nodes' values.

**Example:**

    Input: [1,null,2,3]
       1
        \
         2
        /
       3
    
    Output: [1,3,2]
Follow up: Recursive solution is trivial, could you do it iteratively?

**COMPREHENSION**

顺序遍历二叉树：左-根-右

*方法一* 递归方法：
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
    void inorder(TreeNode* root,vector<int>& res){
        if(!root)
            return;
        if(root->left)
            inorder(root->left,res);
        res.push_back(root->val);
        if(root->right)
            inorder(root->right,res);
    }
};
```

*方法二* 非递归法：：使用栈：：

从根节点开始，先将根节点压入栈，然后再将其所有左子结点压入栈，然后取出栈顶结点，保存节点值，再将当前指针移到右子节点上，若存在右子节点，则在下次循环时，又可将其左子节点压入栈中。

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        TreeNode* p=root;
        stack<TreeNode*> s;
        while(p||!s.empty()){
            while(p){
                s.push(p);
                p=p->left;
            }
            p=s.top();s.pop();
            res.push_back(p->val);
            p=p->right;
        }
        return res;
    }
};
```
