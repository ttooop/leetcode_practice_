>https://leetcode.com/problems/symmetric-tree/

**expression**

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

        1
       / \
      2   2 
     / \ / \
    3  4 4  3
    
**comprehension**

判断二叉树是否是平衡树，可以用递归和迭代两种方法来实现

**递归法**

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
    bool isSymmetric(TreeNode* root) {
        if (!root) {
		      return true;
	      }
	      return isSymmetric(root->left,root->right);
    }
    bool isSymmetric(TreeNode *left, TreeNode *right) {
	      if (!left && !right)
		        return true;
	      if (left && !right || !left&&right || left->val != right->val)
		        return false;
	      return isSymmetric(left->left, right->right) && isSymmetric(left->right, right->left);
    }
};
```
**迭代法**

需要借助两个队列queue实现

首先判空，如果为空，直接返回true。否则将root左右两个子节点分别装入两个队列，然后开始循环，直到两个队列都不为空。在循环中，首先分别将两个队列的队首元素取出来，如果两个都是空结点 ，那么直接跳过，因为还没有比较晚，有可能某个节点没有左子节点，但右子节点仍然存在。

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
    bool isSymmetric(TreeNode* root) {
     if (!root)
		return true;
	queue <TreeNode*> q1, q2;
	q1.push(root->left);
	q2.push(root->right);
	while (!q1.empty() && !q2.empty()) {
		TreeNode *node1 = q1.front(); q1.pop();
		TreeNode *node2 = q2.front(); q2.pop();
		if (!node1 && !node2) continue;
		if ((node1 && !node2) || (!node1 && node2)) return false;
		if (node1->val != node2->val) return false;
		q1.push(node1->left);
		q1.push(node1->right);
		q2.push(node2->right);
		q2.push(node2->left);
		}
		return true;
};
```
