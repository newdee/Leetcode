# 求具有所有最深结点的最小子树
> 给定一个根为 root 的二叉树，每个结点的深度是它到根的最短距离。
如果一个结点在整个树的任意结点之间具有最大的深度，则该结点是最深的。
一个结点的子树是该结点加上它的所有后代的集合。
返回能满足“以该结点为根的子树中包含所有最深的结点”这一条件的具有最大深度的结点。

方法：当左右子树深度相同时，则根子树就是最小子树。当左子树深度大于右子树时，将左子树看做根节点，继续比较左子树的左右子树。同理，右子树也是一样的方法，最后得到所求的最小子树。


通过创建一个函数求子树深度。
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
    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
       int DL= depth(root->left);
        int DR = depth(root->right);
        if (DL == DR)
            return root;
        else
            return DL>DR? subtreeWithAllDeepest(root->left):subtreeWithAllDeepest(root->right);

    }
private:
    int depth(TreeNode* root)
    {
        if(root==NULL)
            return 0;
        int dl = depth(root->left);
        int dr = depth(root->right);
        return dl>dr ? dl+1:dr+1;
    }
};
```
