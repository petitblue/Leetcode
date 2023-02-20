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
##257. Binary Tree Paths

https://leetcode.com/problems/binary-tree-paths/description/

```sh
void getPath(char **array, struct TreeNode* root,int* returnSize, int *buf, int local) {
    if(root == NULL)return;
    if(root->left == NULL && root-> right == NULL) {
        char *str = (char*)malloc(1024);
        int len = 0;
        for(int i  =0;i<local; i++) {
            len += sprintf(str+len, "%d->", buf[i]);

        }
        sprintf(str+len, "%d", root->val);
        array[(*returnSize)++] = str;
    }
    buf[local++] = root->val;
    getPath(array, root->left, returnSize, buf, local);
    getPath(array, root->right, returnSize, buf, local);
}
char ** binaryTreePaths(struct TreeNode* root, int* returnSize){
    char ** res = (char **)malloc(sizeof(char*)*1024);
    *returnSize = 0;
    int buf[1024] ={0};
    getPath(res, root, returnSize, buf, 0);
    return res;

}

```
##404. Sum of Left Leaves
https://leetcode.com/problems/sum-of-left-leaves/
-what's left leaves: node->left, node-> right are null; node is the parent node's left node. 
- that's node->left, and  node->left->left == NULL && node->left->right == NULL
- use post order traveral, as we traverse to the leaves node and return values to the previous level node.
```sh
int sumOfLeftLeaves(struct TreeNode* root){
    if(root == NULL) {
        return 0;
    }
    // when we reach the leaves node, we didn't cound yet, we will to return to the parent node to count the value
    if(root->left == NULL && root->right == NULL){
        return 0;
    }
    int leftNum =0;
    int rightNum =0;
    leftNum = sumOfLeftLeaves(root->left);
    if(root->left != NULL && root->left->left == NULL &&root->left->right == NULL) {
        leftNum = root->left->val;
        
    }
   rightNum = sumOfLeftLeaves(root->right);//right subtrees' left leaves
    
    
    
    return leftNum+rightNum;
}  
```
