## 104. Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/
- figure out the differences between height and depth :   
- the depth of a tree is the root node height, to calculate root node height, we use post-order traversal
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

##111. Minimum Depth of Binary Tree
https://leetcode.com/problems/minimum-depth-of-binary-tree/

```sh
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
int min(int a, int b) {
    if(a<b) {
        return a;
        }
        return b;
    
}
int minDepth(struct TreeNode* root){
   // calculate root to the nearest leaf node's height
   // use post order traversal
   if(root == NULL) {
       return 0;
   }
   int leftHeight = minDepth(root->left);
   int rightHeight = minDepth(root->right);
   int res;
   // if the root left child is null and right child is not null
    if (root->left == NULL && root->right != NULL) {
        return 1+rightHeight;
    }
      // if the root right child is null and left child is not null
    if (root->left != NULL && root->right == NULL) {
        return 1+leftHeight;
    }

   // if both left and right child are not null
   res = 1+min(leftHeight,rightHeight);
   return res;
}
```
##222. Count Complete Tree Nodes

https://leetcode.com/problems/count-complete-tree-nodes/

```sh
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
int countNodes(struct TreeNode* root){
    if (root == NULL) {
        return 0;
    }
    int leftNum = countNodes(root->left);
    int rightNum = countNodes(root->right);
    int num = leftNum + rightNum +1;
    return num;

}
```
- use the concept of complete binatry tree
```sh

// complete binatry tree node number = 2^h-1  h is the height of the tree
 //traverse a subtree's left and right , and check if the left and right height the same, if they are then they are complete binatry tree and can use the formular
 #include<math.h>
int countNodes(struct TreeNode* root){
   if(root == NULL) {
       return 0;
   }
   struct TreeNode* left = root->left;
   struct TreeNode*  right = root->right;
   int leftHeight = 0;
   int rightHeight = 0;
   int num = 0;
   //traverse a subtree's left and right 
   while(left) {
       left = left->left;
       leftHeight ++;
   }
   while(right) {
       right= right->right;
       rightHeight ++;
   }
   // check if the left and right height the same,
   if(leftHeight == rightHeight) {
      num = pow(2,leftHeight) -1;
   }
   //recursion
   int leftNum = countNodes(root->left);
   int rightNum = countNodes(root->right);
   return 1+leftNum+rightNum;
 }
 ```
