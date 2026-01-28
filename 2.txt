#include <stdio.h>

typedef struct {
    int coeff;
    int exp;
} Term;

void display(Term p[], int n) {
    for (int i = 0; i < n; i++) {
        if (i > 0 && p[i].coeff > 0)
            printf("+");
        printf("%dx^%d ", p[i].coeff, p[i].exp);
    }
    printf("\n");
}

int main() {
    Term poly[20], result[20];
    int n1, n2, i, j, k = 0;

    printf("Enter number of terms in Polynomial 1: ");
    scanf("%d", &n1);

    printf("Enter terms (coeff exp) in descending order:\n");
    for (i = 0; i < n1; i++)
        scanf("%d %d", &poly[i].coeff, &poly[i].exp);

    printf("Enter number of terms in Polynomial 2: ");
    scanf("%d", &n2);

    printf("Enter terms (coeff exp) in descending order:\n");
    for (i = n1; i < n1 + n2; i++)
        scanf("%d %d", &poly[i].coeff, &poly[i].exp);

    i = 0;
    j = n1;

    while (i < n1 && j < n1 + n2) {
        if (poly[i].exp == poly[j].exp) {
            result[k].coeff = poly[i].coeff + poly[j].coeff;
            result[k].exp = poly[i].exp;
            i++; j++; k++;
        } 
        else if (poly[i].exp > poly[j].exp) {
            result[k++] = poly[i++];
        } 
        else {
            result[k++] = poly[j++];
        }
    }

    while (i < n1)
        result[k++] = poly[i++];

    while (j < n1 + n2)
        result[k++] = poly[j++];

    printf("Resultant Polynomial: ");
    display(result, k);

    return 0;
}
