#include <stdio.h>
#include <ctype.h>

#define SIZE 50

int stack[SIZE];
int top = -1;

/* Push operation */
void push(int value) {
    stack[++top] = value;
}

/* Pop operation */
int pop() {
    return stack[top--];
}

/* Evaluate postfix expression */
int evaluatePostfix(char postfix[]) {
    int i;
    int op1, op2, result;

    for (i = 0; postfix[i] != '\0'; i++) {

        /* If operand, push to stack */
        if (isdigit(postfix[i])) {
            push(postfix[i] - '0');   // convert char to int
        }

        /* If operator */
        else {
            op2 = pop();
            op1 = pop();

            switch (postfix[i]) {
                case '+': result = op1 + op2; break;
                case '-': result = op1 - op2; break;
                case '*': result = op1 * op2; break;
                case '/': result = op1 / op2; break;
            }

            push(result);
        }
    }

    return pop();   // final result
}

/* Main function */
int main() {
    char postfix[50];
    int result;

    printf("Enter postfix expression: ");
    scanf("%s", postfix);

    result = evaluatePostfix(postfix);

    printf("Result = %d\n", result);

    return 0;
}
