>https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

**EXPRESSION**

Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

    preorder = [3,9,20,15,7]
    inorder = [9,3,15,20,7]

Return the following binary tree:

        3
       / \
      9  20
        /  \
       15   7
       
**COMPREHENSION**

根据先序遍历和中序遍历的结果来建立二叉树。

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return buildtree(preorder,0,preorder.size()-1,inorder,0,inorder.size()-1);
    }
    TreeNode* buildtree(vector<int>& preorder,int pleft,int pright,vector<int>& inorder,int ileft,int iright){
        if(pleft>pright||ileft>iright)
            return NULL;
        int i=0;
        for(i=ileft;i<=iright;++i){
            if(preorder[pleft]==inorder[i])
                break;
        }//找到根节点在inorder中的位置
        TreeNode *cur=new TreeNode(preorder[pleft]);
        cur->left=buildtree(preorder,pleft+1,pleft+i-ileft,inorder,ileft,i-1);
        cur->right=buildtree(preorder,pleft+i-ileft+1,pright,inorder,i+1,iright);
        return cur;
    }
};
```
