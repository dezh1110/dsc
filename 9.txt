#include <stdio.h>
#include <stdlib.h>

/* Structure for queue node */
struct node {
    int data;
    struct node *next;
};

struct node *front = NULL;
struct node *rear = NULL;

/* Add element to queue */
void enqueue(int item) {
    struct node *newNode;

    newNode = (struct node *)malloc(sizeof(struct node));

    if (newNode == NULL) {
        printf("Queue Overflow\n");
        return;
    }

    newNode->data = item;
    newNode->next = NULL;

    if (front == NULL) {   // empty queue
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }

    printf("Inserted %d\n", item);
}

/* Delete element from queue */
void dequeue() {
    struct node *temp;

    if (front == NULL) {
        printf("Queue Underflow\n");
        return;
    }

    temp = front;
    printf("Deleted %d\n", temp->data);
    front = front->next;

    if (front == NULL)   // queue becomes empty
        rear = NULL;

    free(temp);
}

/* Display queue contents */
void display() {
    struct node *temp;

    if (front == NULL) {
        printf("Queue is empty\n");
        return;
    }

    printf("Queue contents: ");
    temp = front;
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
        printf("\n1. Add\n2. Delete\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter item to add: ");
                scanf("%d", &item);
                enqueue(item);
                break;

            case 2:
                dequeue();
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
