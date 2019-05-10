>https://leetcode.com/problems/path-sum-iii/

**expression**

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

    root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

          10
         /  \
        5   -3
       / \    \
      3   2   11
     / \   \
    3  -2   1
    
    Return 3. The paths that sum to 8 are:
    
    1.  5 -> 3
    2.  5 -> 2 -> 1
    3. -3 -> 11
    
**comprehension**

求二叉树的路径的和等于一个给定值，该路径不必要从根节点开始，可以是中间的任意一段。。可以用递归来做，相当于先序遍历二叉树，对于每一个节点都记录了一条从根节点到当前结点的路径，同时用一个变量cursum记录路径节点总和，然后看cursum和sum是否相等，相等的话结果加以，不等的话继续检查查看子路径有没有满足题意，做法就是每次去掉一个节点，看路径和是否等于给定值，注意最后必须留一个节点，不能全丢掉了，如果全去掉，路径之和为0，如果给定值刚好为0的话就会有问题

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
    int pathSum(TreeNode* root, int sum) {
        int res=0;
        vector<TreeNode*> out;
        helper(root,sum,0,out,res);
        return res;
    }
    void helper(TreeNode* node,int sum,int cursum,vector<TreeNode*>& out,int& res){
        if(!node)
            return ;
        cursum+=node->val;
        out.push_back(node);
        if(sum==cursum)
            ++res;
        int t=cursum;
        for(int i=0;i<out.size()-1;++i){
            t-=out[i]->val;
            if(t==sum)
                ++res;
        }
        helper(node->left,sum,cursum,out,res);
        helper(node->right,sum,cursum,out,res);
        out.pop_back();
    }
};
```
