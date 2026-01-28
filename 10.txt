#include <stdio.h>
#include <stdlib.h>

/* Structure for polynomial node */
struct node {
    int coeff;
    int exp;
    struct node *next;
};

/* Create a polynomial */
struct node* createPoly(int n) {
    struct node *head = NULL, *temp = NULL, *newNode;
    int i;

    for (i = 0; i < n; i++) {
        newNode = (struct node *)malloc(sizeof(struct node));

        printf("Enter coefficient and exponent: ");
        scanf("%d %d", &newNode->coeff, &newNode->exp);
        newNode->next = NULL;

        if (head == NULL) {
            head = temp = newNode;
        } else {
            temp->next = newNode;
            temp = newNode;
        }
    }
    return head;
}

/* Add two polynomials */
struct node* addPoly(struct node *p1, struct node *p2) {
    struct node *result = NULL, *temp = NULL, *newNode;

    while (p1 != NULL && p2 != NULL) {
        newNode = (struct node *)malloc(sizeof(struct node));
        newNode->next = NULL;

        if (p1->exp == p2->exp) {
            newNode->coeff = p1->coeff + p2->coeff;
            newNode->exp = p1->exp;
            p1 = p1->next;
            p2 = p2->next;
        } 
        else if (p1->exp > p2->exp) {
            newNode->coeff = p1->coeff;
            newNode->exp = p1->exp;
            p1 = p1->next;
        } 
        else {
            newNode->coeff = p2->coeff;
            newNode->exp = p2->exp;
            p2 = p2->next;
        }

        if (result == NULL) {
            result = temp = newNode;
        } else {
            temp->next = newNode;
            temp = newNode;
        }
    }

    /* Copy remaining terms */
    while (p1 != NULL) {
        newNode = (struct node *)malloc(sizeof(struct node));
        newNode->coeff = p1->coeff;
        newNode->exp = p1->exp;
        newNode->next = NULL;
        temp->next = newNode;
        temp = newNode;
        p1 = p1->next;
    }

    while (p2 != NULL) {
        newNode = (struct node *)malloc(sizeof(struct node));
        newNode->coeff = p2->coeff;
        newNode->exp = p2->exp;
        newNode->next = NULL;
        temp->next = newNode;
        temp = newNode;
        p2 = p2->next;
    }

    return result;
}

/* Display polynomial */
void display(struct node *poly) {
    while (poly != NULL) {
        printf("%dx^%d", poly->coeff, poly->exp);
        if (poly->next != NULL)
            printf(" + ");
        poly = poly->next;
    }
    printf("\n");
}

/* Main function */
int main() {
    struct node *poly1, *poly2, *poly3;
    int n1, n2;

    printf("Enter number of terms in Polynomial 1: ");
    scanf("%d", &n1);
    poly1 = createPoly(n1);

    printf("Enter number of terms in Polynomial 2: ");
    scanf("%d", &n2);
    poly2 = createPoly(n2);

    printf("\nPolynomial 1: ");
    display(poly1);

    printf("Polynomial 2: ");
    display(poly2);

    poly3 = addPoly(poly1, poly2);

    printf("Resultant Polynomial: ");
    display(poly3);

    return 0;
}
