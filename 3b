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

/* Fast Transpose */
void fastTranspose(Sparse a[], Sparse b[]) {
    int row_terms[20], start_pos[20];
    int i, j;

    b[0].row = a[0].col;
    b[0].col = a[0].row;
    b[0].val = a[0].val;

    for (i = 0; i < a[0].col; i++)
        row_terms[i] = 0;

    for (i = 1; i <= a[0].val; i++)
        row_terms[a[i].col]++;

    start_pos[0] = 1;
    for (i = 1; i < a[0].col; i++)
        start_pos[i] = start_pos[i - 1] + row_terms[i - 1];

    for (i = 1; i <= a[0].val; i++) {
        j = start_pos[a[i].col]++;
        b[j].row = a[i].col;
        b[j].col = a[i].row;
        b[j].val = a[i].val;
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

    fastTranspose(a, b);

    printf("\nTransposed Sparse Matrix:\n");
    display(b);

    return 0;
}
