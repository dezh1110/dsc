#include <stdio.h>
#include <stdlib.h>

int *queue;
int front = -1, rear = -1, size;

/* Insert element into circular queue */
void enqueue(int item) {
    if ((front == (rear + 1) % size)) {
        printf("Queue Overflow\n");
        return;
    }

    if (front == -1) {   // first element
        front = 0;
        rear = 0;
    } else {
        rear = (rear + 1) % size;
    }

    queue[rear] = item;
    printf("Inserted %d\n", item);
}

/* Delete element from circular queue */
void dequeue() {
    int item;

    if (front == -1) {
        printf("Queue Underflow\n");
        return;
    }

    item = queue[front];
    printf("Deleted %d\n", item);

    if (front == rear) {   // only one element
        front = rear = -1;
    } else {
        front = (front + 1) % size;
    }
}

/* Display circular queue */
void display() {
    int i;

    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }

    printf("Queue contents: ");
    i = front;
    while (1) {
        printf("%d ", queue[i]);
        if (i == rear)
            break;
        i = (i + 1) % size;
    }
    printf("\n");
}

/* Main function */
int main() {
    int choice, item;

    printf("Enter size of circular queue: ");
    scanf("%d", &size);

    queue = (int *)malloc(size * sizeof(int));

    if (queue == NULL) {
        printf("Memory allocation failed\n");
        return 0;
    }

    while (1) {
        printf("\n1. Insert\n2. Delete\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter item to insert: ");
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
                free(queue);
                exit(0);

            default:
                printf("Invalid choice\n");
        }
    }

    return 0;
}
