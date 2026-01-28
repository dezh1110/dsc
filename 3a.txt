#include <stdio.h>

typedef struct {
    int row;
    int col;
    int val;
} Sparse;

/* Display Sparse Matrix */
void display(Sparse a[]) {
    int i;
    printf("Row  Col  Val\n");
    for (i = 0; i <= a[0].val; i++)
        printf("%d    %d    %d\n", a[i].row, a[i].col, a[i].val);
}

/* Simple Transpose */
void simpleTranspose(Sparse a[], Sparse b[]) {
    int i, j, k = 1;

    b[0].row = a[0].col;
    b[0].col = a[0].row;
    b[0].val = a[0].val;

    for (i = 0; i < a[0].col; i++) {
        for (j = 1; j <= a[0].val; j++) {
            if (a[j].col == i) {
                b[k].row = a[j].col;
                b[k].col = a[j].row;
                b[k].val = a[j].val;
                k++;
            }
        }
    }
}

int main() {
    Sparse a[20], b[20];
    int i;

    printf("Enter rows, columns and non-zero elements: ");
    scanf("%d %d %d", &a[0].row, &a[0].col, &a[0].val);

    printf("Enter row col value:\n");
    for (i = 1; i <= a[0].val; i++)
        scanf("%d %d %d", &a[i].row, &a[i].col, &a[i].val);

    printf("\nOriginal Sparse Matrix:\n");
    display(a);

    simpleTranspose(a, b);

    printf("\nTransposed Sparse Matrix:\n");
    display(b);

    return 0;
}
