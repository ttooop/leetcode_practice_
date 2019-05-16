>https://leetcode.com/problems/binary-tree-level-order-traversal/

**EXPRESSION**

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

**For example:**

    Given binary tree [3,9,20,null,null,15,7],
        3
       / \
      9  20
        /  \
       15   7
    return its level order traversal as:
    [
      [3],
      [9,20],
      [15,7]
    ]
    
**COMPREHENSION**

层序遍历二叉树是典型的广度优先搜索BFS的应用

*方法一* 非递归法：：建立一个queue，把根节点放进去，找根节点左右两个子节点，去掉根节点此时queue里的元素就是下一层的所有结点，用一个for循环遍历它们，然后存到一个一维向量里，遍历完之后再把这个一维向量存到二维向量里，以此类推。

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(!root)
            return {};
        vector<vector<int>> res;
        queue<TreeNode*> q{{root}};
        while(!q.empty()){
            vector<int> one;
            for(int i=q.size();i>0;--i){
                TreeNode *t=q.front();q.pop();
                one.push_back(t->val);
                if(t->left)
                    q.push(t->left);
                if(t->right)
                    q.push(t->right);
            }
            res.push_back(one);
        }
        return res;
    }
};
```

*方法二* 递归法

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        levelorder(root,0,res);
        return res;
    }
    void levelorder(TreeNode* root,int level,vector<vector<int>>& res){
        if(!root)
            return;
        if(res.size()==level)
            res.push_back({});
        res[level].push_back(root->val);
        if(root->left)
            levelorder(root->left,level+1,res);
        if(root->right)
            levelorder(root->right,level+1,res);
    }
};
```
