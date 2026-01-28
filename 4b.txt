#include <stdio.h>
#include <string.h>

void nfind(char text[], char pat[]) {
    int n = strlen(text);
    int m = strlen(pat);
    int i, j;

    for (i = 0; i <= n - m; i++) {
        for (j = 0; j < m; j++) {
            if (text[i + j] != pat[j])
                break;
        }
        if (j == m)
            printf("Pattern found at position %d\n", i);
    }
}

int main() {
    char text[100], pat[50];

    printf("Enter the text: ");
    scanf("%s", text);

    printf("Enter the pattern: ");
    scanf("%s", pat);

    nfind(text, pat);

    return 0;
}
