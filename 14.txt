#include <stdio.h>

#define MAX 20

int graph[MAX][MAX];
int visited[MAX];
int n;

/* DFS traversal */
void DFS(int v) {
    int i;
    visited[v] = 1;
    printf("%d ", v);

    for (i = 0; i < n; i++) {
        if (graph[v][i] == 1 && visited[i] == 0) {
            DFS(i);
        }
    }
}

/* BFS traversal */
void BFS(int start) {
    int queue[MAX], front = 0, rear = -1;
    int i;
    int visitedBFS[MAX] = {0};

    queue[++rear] = start;
    visitedBFS[start] = 1;

    while (front <= rear) {
        int v = queue[front++];
        printf("%d ", v);

        for (i = 0; i < n; i++) {
            if (graph[v][i] == 1 && visitedBFS[i] == 0) {
                queue[++rear] = i;
                visitedBFS[i] = 1;
            }
        }
    }
}

/* Main function */
int main() {
    int i, j, start;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter adjacency matrix:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            scanf("%d", &graph[i][j]);
        }
    }

    for (i = 0; i < n; i++)
        visited[i] = 0;

    printf("Enter starting vertex for DFS: ");
    scanf("%d", &start);
    printf("DFS Traversal: ");
    DFS(start);

    printf("\nEnter starting vertex for BFS: ");
    scanf("%d", &start);
    printf("BFS Traversal: ");
    BFS(start);

    return 0;
}
