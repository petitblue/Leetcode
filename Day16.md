## 104. Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/
- figure out the differences between height and depth :   
- the depth of a tree is the root node height, to calculate root node height, we use post order traversal
- its more straight forwards to calculate the height here


```sh
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
int max(int a, int b) {
    if(a>b) {
        return a;
    }
    return b;
}
int maxDepth(struct TreeNode* root){
    if (root == NULL) {
        return 0;
    }
    int leftHeight = maxDepth(root->left);
    int  rightHeight = maxDepth(root->right);
    int height= 1+max(leftHeight,rightHeight);
    // the maxdepth equals to the max height of the tree
    return height;

}

```
