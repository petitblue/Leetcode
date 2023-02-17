### 226. Invert Binary Tree
/ Problem #: 226. Invert Binary Tree
// Level: Easy
// Link: https://leetcode.com/problems/invert-binary-tree/
// Name: Luyan Deng

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
struct TreeNode* invertTree(struct TreeNode* root){
    if ( root == NULL) {
        return root;
    }
    // if root is not null, swap the children
    struct TreeNode* temp = root->left;
    root->left = root->right;
    root->right = temp;
    invertTree(root->left);
    invertTree(root->right);
    return root;
}
### 101. Symmetric Tree
https://leetcode.com/problems/symmetric-tree/


```sh
**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
//syemmetric means that the root->left  == root->right 
bool symmetric(struct TreeNode* left, struct TreeNode* right) {
    if(left == NULL && right == NULL){
        return true;
    }else if(left == NULL && right != NULL) {
        return false;
    }else if(left != NULL && right == NULL) {
        return false;
    }
    else if(left->val != right->val) {
        return false;
    }
    return symmetric(left->left,right->right) && symmetric(left->right, right->left);
}
bool isSymmetric(struct TreeNode* root){
   if(root == NULL) {
       return true;
   }
   return symmetric(root->left,root->right);
}
```
