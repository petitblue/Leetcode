## 513. Find Bottom Left Tree Value
https://leetcode.com/problems/find-bottom-left-tree-value/
- find the bottom left, we will find the maximum depth of the tree, and get the left value
- note that the bottom left value is not nessesariy the left leaves
- when we use recursion, we use the backtracking too. so we will increase the depth first and then decrease the depth,
- so we can come back and recalculate the depth again.
```sh
int traversal (struct TreeNode* root,int depth, int* maxdepth, int* result){
        if(root == NULL){return 0;}
        //traveral to the leaves and update depth of the tree
        if(root->left == NULL && root->right == NULL) {
            if(depth > *maxdepth) {
                *maxdepth = depth;
                *result = root->val;
            }
        }
        if(root->left){
            depth++;
            traversal(root->left,depth,maxdepth,result);
            depth --;
        }
        if(root->right){
            depth++;
            traversal(root->right,depth,maxdepth,result);
            depth--;
        }
        return *result;
    }
int findBottomLeftValue(struct TreeNode* root){

    int max = INT_MIN;
    int result =0;
    
    result = traversal(root, 0,&max,&result);
    return result;

}
```
