>https://leetcode.com/problems/validate-binary-search-tree/

**EXPRESSION**

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.
 
**Example 1:**

        2
       / \
      1   3
    
    Input: [2,1,3]
    Output: true
**Example 2:**

        5
       / \
      1   4
         / \
        3   6
    
    Input: [5,1,4,null,null,3,6]
    Output: false
    Explanation: The root node's value is 5 but its right child's value is 4.

**COMPREHENSION**

判断是否是最大根二叉树。

*方法一* 递归法

先通过递归实现顺序遍历（左-根-右），并将值保存在vals数组中，然后循环数组vals，查看是否是由小到大，若否则返回false。

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
    bool isValidBST(TreeNode* root) {
        if(!root)
            return true;
        vector<int> vals;
        inorder(root,vals);
        for(int i=0;i<vals.size()-1;++i){
            if(vals[i]>=vals[i+1])
                return false;
        }
        return true;
    }
    void inorder(TreeNode* root,vector<int>& vals){
        if(!root)
            return;
        inorder(root->left,vals);
        vals.push_back(root->val);
        inorder(root->right,vals);
    }
};
```

*方法二* 非递归法：：使用栈
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
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> s;
        TreeNode *p=root,*pre=NULL;
        while(p||!s.empty()){
            while(p){
                s.push(p);
                p=p->left;
            }
            p=s.top();s.pop();
            if(pre&&p->val<=pre->val)
                return false;
            pre=p;
            p=p->right;
        }
        return true;
    }
};
```
