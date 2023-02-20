## 110. Balanced Binary Tree

https://leetcode.com/problems/balanced-binary-tree/

```sh
int max(int a, int b) {
    if(a>b) {
        return a;
    }
    return b;
}
int height(struct TreeNode* root) {
    if(root == NULL) {return 0;}
    int leftHeight = height(root->left);
    if(leftHeight == -1) return -1;
    int rightHeight = height(root->right);
    if(rightHeight == -1) return -1;
    int height = max(leftHeight,rightHeight)+1;
    return height;
}
bool isBalanced(struct TreeNode* root){
   if(root == NULL) {
       return true;
       }
    int left = height(root->left);
    int right = height(root->right);
    int diff = left-right;
    if(diff > 1 || diff < -1) {
        return false;
    }else{
        return isBalanced(root->left)&&isBalanced(root->right);
    }

}
```
