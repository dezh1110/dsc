#include <stdio.h>
#include <ctype.h>

#define SIZE 50

/* Stack declaration */
char stack[SIZE];
int top = -1;

/* Push operation */
void push(char ch) {
    stack[++top] = ch;
}

/* Pop operation */
char pop() {
    return stack[top--];
}

/* Function to check precedence */
int precedence(char ch) {
    if (ch == '+' || ch == '-')
        return 1;
    if (ch == '*' || ch == '/')
        return 2;
    if (ch == '^')
        return 3;
    return 0;
}

/* Function to convert infix to postfix */
void infixToPostfix(char infix[], char postfix[]) {
    int i = 0, j = 0;
    char ch, x;

    while ((ch = infix[i++]) != '\0') {

        /* If operand, add to postfix */
        if (isalnum(ch)) {
            postfix[j++] = ch;
        }

        /* If left parenthesis, push to stack */
        else if (ch == '(') {
            push(ch);
        }

        /* If right parenthesis, pop until '(' */
        else if (ch == ')') {
            while ((x = pop()) != '(')
                postfix[j++] = x;
        }

        /* If operator */
        else {
            while (top != -1 && precedence(stack[top]) >= precedence(ch))
                postfix[j++] = pop();
            push(ch);
        }
    }

    /* Pop remaining operators from stack */
    while (top != -1)
        postfix[j++] = pop();

    postfix[j] = '\0';
}

/* Main function */
int main() {
    char infix[50], postfix[50];

    printf("Enter infix expression: ");
    scanf("%s", infix);

    infixToPostfix(infix, postfix);

    printf("Postfix expression: %s\n", postfix);

    return 0;
}
