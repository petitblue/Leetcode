Tree Traversal

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

#define MAX_STRING 200

// ========================== TREE DEFINITIONS ==========================
// define tree node structure 
typedef struct tnd {
  char data;
  struct tnd* left;
  struct tnd* right;
} tnode_t;

// "new" function to create a tree node, set data value to d and childrent to NULL
tnode_t* newTNode(char d) {
  tnode_t* np;
  np = (tnode_t*)malloc(sizeof(tnode_t));
  if (np != NULL) {
    np->data = d;
    np->left = NULL;
    np->right = NULL;
  }
  return(np);
}

// free a tree node and all its children
void freeTNode(tnode_t* np) {
  if (np != NULL) {
    freeTNode(np->left);
    freeTNode(np->right);
    free(np);
  }
                     
void preorder (tnode_t* np) {
  // INSERT YOUR CODE HERE
  if(np == NULL) {
    return;
  }
  printf("%c",np->data);
    preorder(np->left);
    preorder(np->right);

 return;
}

void inorder (tnode_t* np) {
  // INSERT YOUR CODE HERE
 if(np == NULL) {
    return;
  }
  inorder(np->left);
  printf("%c",np->data);
  inorder(np->right);
  return;
}

void postorder (tnode_t* np) {
  // INSERT YOUR CODE HERE
  if(np == NULL) {
    return;
  }
  postorder (np->left);
  postorder (np->right);
  printf("%c",np->data);
  return;
}

