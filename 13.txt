#include <stdio.h>

#define MAX 50

int heap[MAX];
int size = 0;

/* Swap function */
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

/* Insert element into max heap */
void insert(int item) {
    int i;

    if (size == MAX) {
        printf("Heap Overflow\n");
        return;
    }

    heap[size] = item;
    i = size;
    size++;

    /* Heapify-up */
    while (i != 0 && heap[(i - 1) / 2] < heap[i]) {
        swap(&heap[i], &heap[(i - 1) / 2]);
        i = (i - 1) / 2;
    }

    printf("Inserted %d\n", item);
}

/* Delete root element from max heap */
void delete() {
    int i = 0;

    if (size == 0) {
        printf("Heap Underflow\n");
        return;
    }

    printf("Deleted %d\n", heap[0]);

    heap[0] = heap[size - 1];
    size--;

    /* Heapify-down */
    while (1) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < size && heap[left] > heap[largest])
            largest = left;

        if (right < size && heap[right] > heap[largest])
            largest = right;

        if (largest != i) {
            swap(&heap[i], &heap[largest]);
            i = largest;
        } else
            break;
    }
}

/* Display heap contents */
void display() {
    int i;

    if (size == 0) {
        printf("Heap is empty\n");
        return;
    }

    printf("Heap contents: ");
    for (i = 0; i < size; i++)
        printf("%d ", heap[i]);
    printf("\n");
}

/* Main function */
int main() {
    int choice, item;

    while (1) {
        printf("\n1. Insert\n2. Delete\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter item to insert: ");
                scanf("%d", &item);
                insert(item);
                break;

            case 2:
                delete();
                break;

            case 3:
                display();
                break;

            case 4:
                return 0;

            default:
                printf("Invalid choice\n");
        }
    }
}
