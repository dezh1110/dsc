#include <stdio.h>
#include <stdlib.h>

/* Structure of TBT node */
struct node {
    int data;
    struct node *left, *right;
    int lthread, rthread;
};

/* Create a new node */
struct node* createNode(int item) {
    struct node *newNode = (struct node*)malloc(sizeof(struct node));
    newNode->data = item;
    newNode->left = newNode->right = NULL;
    newNode->lthread = 1;
    newNode->rthread = 1;
    return newNode;
}

/* Insert node into Inorder Threaded Binary Tree */
struct node* insert(struct node *root, int item) {
    struct node *ptr = root;
    struct node *parent = NULL;

    while (ptr != NULL) {
        parent = ptr;

        if (item < ptr->data) {
            if (ptr->lthread == 0)
                ptr = ptr->left;
            else
                break;
        } else if (item > ptr->data) {
            if (ptr->rthread == 0)
                ptr = ptr->right;
            else
                break;
        } else {
            printf("Duplicate key not allowed\n");
            return root;
        }
    }

    struct node *newNode = createNode(item);

    if (parent == NULL) {
        root = newNode;
    }
    else if (item < parent->data) {
        newNode->left = parent->left;
        newNode->right = parent;
        parent->lthread = 0;
        parent->left = newNode;
    }
    else {
        newNode->right = parent->right;
        newNode->left = parent;
        parent->rthread = 0;
        parent->right = newNode;
    }

    return root;
}

/* Find inorder successor */
struct node* inorderSuccessor(struct node *ptr) {
    if (ptr->rthread == 1)
        return ptr->right;

    ptr = ptr->right;
    while (ptr->lthread == 0)
        ptr = ptr->left;

    return ptr;
}

/* Inorder traversal using threading */
void inorder(struct node *root) {
    struct node *ptr = root;

    if (ptr == NULL) {
        printf("Tree is empty\n");
        return;
    }

    while (ptr->lthread == 0)
        ptr = ptr->left;

    while (ptr != NULL) {
        printf("%d ", ptr->data);
        ptr = inorderSuccessor(ptr);
    }
}

/* Main function */
int main() {
    struct node *root = NULL;
    int n, item, i;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for (i = 0; i < n; i++) {
        scanf("%d", &item);
        root = insert(root, item);
    }

    printf("\nInorder Traversal using Threading: ");
    inorder(root);

    return 0;
}
