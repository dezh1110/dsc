#include <stdio.h>
#include <stdlib.h>

/* Structure for stack node */
struct node {
    int data;
    struct node *next;
};

struct node *top = NULL;

/* Push operation */
void push(int item) {
    struct node *newNode;

    newNode = (struct node *)malloc(sizeof(struct node));

    if (newNode == NULL) {
        printf("Stack Overflow\n");
        return;
    }

    newNode->data = item;
    newNode->next = top;
    top = newNode;

    printf("Pushed %d\n", item);
}

/* Pop operation */
void pop() {
    struct node *temp;

    if (top == NULL) {
        printf("Stack Underflow\n");
        return;
    }

    temp = top;
    printf("Popped %d\n", temp->data);
    top = top->next;
    free(temp);
}

/* Display stack contents */
void display() {
    struct node *temp;

    if (top == NULL) {
        printf("Stack is empty\n");
        return;
    }

    printf("Stack contents: ");
    temp = top;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

/* Main function */
int main() {
    int choice, item;

    while (1) {
        printf("\n1. Push\n2. Pop\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter item to push: ");
                scanf("%d", &item);
                push(item);
                break;

            case 2:
                pop();
                break;

            case 3:
                display();
                break;

            case 4:
                exit(0);

            default:
                printf("Invalid choice\n");
        }
    }

    return 0;
}
