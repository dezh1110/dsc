#include <stdio.h>
#include <string.h>

/* Compute LPS Array */
void computeLPS(char pat[], int m, int lps[]) {
    int len = 0;
    lps[0] = 0;
    int i = 1;

    while (i < m) {
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0)
                len = lps[len - 1];
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

/* KMP Pattern Matching */
void KMP(char text[], char pat[]) {
    int n = strlen(text);
    int m = strlen(pat);
    int lps[50];

    computeLPS(pat, m, lps);

    int i = 0, j = 0;

    while (i < n) {
        if (text[i] == pat[j]) {
            i++;
            j++;
        }

        if (j == m) {
            printf("Pattern found at position %d\n", i - j);
            j = lps[j - 1];
        } 
        else if (i < n && text[i] != pat[j]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i++;
        }
    }
}

int main() {
    char text[100], pat[50];

    printf("Enter the text: ");
    scanf("%s", text);

    printf("Enter the pattern: ");
    scanf("%s", pat);

    KMP(text, pat);

    return 0;
}
