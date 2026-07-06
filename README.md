1 a) 




#include <stdio.h> 
#include <string.h> 

// Function to implement the Naive String Matching Algorithm (Brute Force Approach) 
void naiveStringMatch(char text[], char pattern[]) 
{ 
    int n = strlen(text);     // Length of the text 
    int m = strlen(pattern);  // Length of the pattern 

    // Traverse the text 
    for (int i = 0; i <= n - m; i++)  
    { 
        int j = 0; 

        // Check for the pattern match at position i 
        while (j < m && text[i + j] == pattern[j]) { 
            j++; 
        } 

        // If the full pattern is matched 
        if (j == m)  
        { 
            printf("Pattern found at index %d\n", i); 
        } 
    } 
} 

int main()  
{ 
    // Buffers to store user input strings
    char text[100]; 
    char pattern[50]; 

    // Accept text input from user
    printf("Enter the text: ");
    scanf("%99s", text); 

    // Accept pattern input from user
    printf("Enter the pattern to search: ");
    scanf("%49s", pattern); 

    // Call the function to find pattern in text 
    naiveStringMatch(text, pattern); 

    return 0; 
}






1b )


#include <stdio.h> 
int iterativeBinarySearch(int arr[], int n, int target) { 
    int left = 0, right = n - 1; 
 
    // Repeat while the left index is less than or equal to the right index 
    while (left <= right) { 
        int mid = left + (right - left) / 2; 
 
        // If the target is found at mid 
        if (arr[mid] == target) { 
            return mid; // Return the index 
        } 
 
        // If the target is smaller, ignore the right half 
        if (arr[mid] > target) { 
            right = mid - 1; 
        } 
        // If the target is larger, ignore the left half 
        else { 
            left = mid + 1; 
        } 
    } 
 
    // Target not found 
    return -1; 
} 
 
int main() { 
    int arr[] = {1, 3, 5, 7, 9, 11, 13, 15, 17}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int target = 7; 
 
    int result = iterativeBinarySearch(arr, n, target); 
 
    if (result != -1) 
 { 
        printf("Target %d found at index %d\n", target, result); 
    } else { 
        printf("Target %d not found in the array\n", target); 
    } 
    return 0; 
} 





2) 



#include<stdio.h>
#include<stdlib.h>

int count;

void merge(int a[10], int left, int mid, int right)
{
    int i, j, k, b[10];

    i = left;
    j = mid+1;
    k = left;
    while( (i<=mid) && (j<=right))
    {
        count++;
        if(a[i] < a[j])
        {
            b[k++] = a[i++];
        }
        else
        {
            b[k++] = a[j++];
        }
    }
    while(i <= mid)
    b[k++] = a[i++];
    while(j <= right)
    b[k++] = a[j++];
    for(i=left; i<=right; i++)
    a[i] = b[i];
}
void mergesort(int a[10], int left, int right)
{
    int mid;
    if(left < right)
    {
        mid = (left + right)/2;
        mergesort(a,left,mid);
        mergesort(a,mid+1,right);
        merge(a,left,mid,right);
    }
}

int main()
{
    int i,j,n,a[10];
    printf("\n Enter no of elements: "); scanf("%d",&n);
    printf("\nEnter elements\n");
    for(i=0;i<n;i++)
        scanf("%d",&a[i]);
    mergesort(a,0,n-1);
    printf("\n Sorted elements:\n"); for(i=0;i<n;i++)
        printf("%d\n",a[i]);
    printf("\n Number of counts : %d\n",count); return 0;
}

 





3) QUICKSORT




#include <stdio.h>

// Helper function to swap two elements
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Lomuto partition scheme: uses the last element as the pivot
int partition(int a[], int low, int high) {
    int pivot = a[high]; 
    int i = low - 1;     

    for (int j = low; j < high; j++) {
        if (a[j] < pivot) {
            i++;
            swap(&a[i], &a[j]);
        }
    }
    swap(&a[i + 1], &a[high]);
    return (i + 1);
}

// Recursive QuickSort function
void quicksort(int a[], int low, int high) {
    if (low < high) {
        int pi = partition(a, low, high);
        quicksort(a, low, pi - 1);  // Left subarray
        quicksort(a, pi + 1, high); // Right subarray
    }
}

int main() {
    int n;

    // 1. Get the total number of elements
    printf("Enter number of elements: ");
    if (scanf("%d", &n) != 1 || n <= 0) {
        printf("Invalid array size.\n");
        return 1;
    }

    int a[n]; // Create a variable-length array

    // 2. Read elements from the user
    printf("Enter %d integers:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }

    // 3. Sort the array
    quicksort(a, 0, n - 1);

    // 4. Output the sorted result
    printf("\nSorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", a[i]);
    }
    printf("\n");

    return 0;
}










4 a) 



#include <stdio.h>

// Standard Depth First Search
void dfs(int a[10][10], int n, int v[10], int source) {
    v[source] = 1; // Mark current vertex as visited

    for (int i = 1; i <= n; i++) {
        // If an adjacent vertex is unvisited, explore it
        if (a[source][i] == 1 && v[i] == 0) {
            dfs(a, n, v, i);
        }
    }
}

int main() {
    int n, a[10][10], v[10];
    int is_connected = 1;


    printf("Enter the number of vertices: ");
    scanf("%d", &n);

   
    printf("Enter the Adjacency matrix (0 or 1):\n");
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            scanf("%d", &a[i][j]);
        }
    }

    
    for (int i = 1; i <= n; i++) {
        v[i] = 0;
    }

       dfs(a, n, v, 1);

    for (int i = 1; i <= n; i++) {
        if (v[i] == 0) {
            is_connected = 0; // Found an unreached node
            break;
        }
    }

    if (is_connected) {
        printf("\nThe graph is connected.\n");
    } else {
        printf("\nThe graph is NOT connected.\n");
    }

    return 0;
}



4b)





#include <stdio.h>
#include <stdlib.h>
#define MAX 100 // Maximum number of vertices in the graph
// Function prototypes
void BFS(int graph[MAX][MAX], int n, int start);
int main() {
    int n, i, j, start;
    int graph[MAX][MAX]; // Adjacency matrix representation of the graph
    printf("Enter the number of vertices: ");
    scanf("%d", &n);
    printf("Enter the adjacency matrix of the graph:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            scanf("%d", &graph[i][j]);
        }
    }
    printf("Enter the starting vertex: ");
    scanf("%d", &start);
    printf("Nodes reachable from vertex %d using BFS:\n", start);
    BFS(graph, n, start);

    return 0;
}

// Breadth-First Search function
void BFS(int graph[MAX][MAX], int n, int start) {
    int visited[MAX] = {0}; // Array to track visited vertices
    int queue[MAX];         // Queue for BFS traversal
    int front = 0, rear = 0;
    // Mark the starting vertex as visited and enqueue it
    visited[start] = 1;
    queue[rear++] = start;
    while (front < rear) {
        // Dequeue a vertex from the queue
        int current = queue[front++];
        printf("%d ", current); // Print the current vertex
        // Enqueue all unvisited neighbors of the current vertex
        for (int i = 0; i < n; i++) {
            if (graph[current][i] == 1 && !visited[i]) {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
}







5) topological




#include <stdio.h>

#define MAX 10

int adj[MAX][MAX];
int visited[MAX];
int topo_stack[MAX];
int top = -1;

void dfs(int u, int n) {
    visited[u] = 1;

    for (int v = 0; v < n; v++) {
        if (adj[u][v] == 1 && !visited[v]) {
            dfs(v, n);
        }
    }
    // Inline push operation
    topo_stack[++top] = u;
}

int main() {
    int n, edges, u, v;

    printf("Enter number of vertices and edges: ");
    scanf("%d %d", &n, &edges);

    printf("Enter edges (source destination):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        adj[u][v] = 1;
    }

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i, n);
        }
    }

    printf("\nTopological Order: ");
    while (top >= 0) {
        printf("%d ", topo_stack[top--]);
    }
    printf("\n");

    return 0;
}







6)



#include <stdio.h>
#include <string.h>
#define MAX 256 // Maximum size for the alphabet

// Function to create the shift table
void createShiftTable(char *pattern, int patternLength, int shiftTable[]) {
    for (int i = 0; i < MAX; i++) {
        shiftTable[i] = patternLength; // Default shift value is the length of the pattern
    }
    for (int i = 0; i < patternLength - 1; i++) {
        shiftTable[(unsigned char)pattern[i]] = patternLength - 1 - i;
    }
}

// Function to implement Horspool's string matching algorithm
int horspoolMatching(char *text, char *pattern) {
    int textLength = strlen(text);
    int patternLength = strlen(pattern);
    int shiftTable[MAX];
    createShiftTable(pattern, patternLength, shiftTable);
    int i = patternLength - 1; // Start with the end of the first window
    while (i < textLength) {
        int k = 0;
        // Compare the pattern from right to left
        while (k < patternLength && pattern[patternLength - 1 - k] == text[i - k]) {
            k++;
        }
        if (k == patternLength) { // Match found
            return i - patternLength + 1;
        } else { // Shift based on the shift table
            i += shiftTable[(unsigned char)text[i]];
        }
    }
    return -1; // No match found
}

int main() {
    char text[100], pattern[50];
    printf("Enter the text: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0'; // Remove newline character
    printf("Enter the pattern: ");
    fgets(pattern, sizeof(pattern), stdin);
    pattern[strcspn(pattern, "\n")] = '\0'; // Remove newline character
    int position = horspoolMatching(text, pattern);
    
    if (position != -1) {
        printf("Pattern found at position: %d\n", position);
    } else {
        printf("Pattern not found in the text.\n");
    }
    return 0;
}




7)


#include<stdio.h>

void warsh(int p[][10], int n)
{
    int i, j, k;
    for(k = 1; k <= n; k++)
        for(i = 1; i <= n; i++)
            for(j = 1; j <= n; j++)
                p[i][j] = p[i][j] || p[i][k] && p[k][j];
}

int main()
{
    int a[10][10], n, i, j;
    printf("\nEnter the n value: ");
    scanf("%d", &n);
    printf("\nEnter the graph data:\n");
    for(i = 1; i <= n; i++)
        for(j = 1; j <= n; j++)
            scanf("%d", &a[i][j]);
    warsh(a, n);
    printf("\nResultant path matrix\n");
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <= n; j++)
            printf("%d ", a[i][j]);
        printf("\n");
    }
    return 0;
}







8)



#include <stdio.h>

#define INF 999 // Represents infinity (no direct edge)

void floyd(int p[10][10], int n) {
    // k is the intermediate vertex, i is source, j is destination
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // Only update if paths through k actually exist (prevents overflow)
                if (p[i][k] != INF && p[k][j] != INF) {
                    if (p[i][k] + p[k][j] < p[i][j]) {
                        p[i][j] = p[i][k] + p[k][j];
                    }
                }
            }
        }
    }
}

int main() {
    int a[10][10], n;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter graph weights (use 999 for infinity):\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &a[i][j]);
        }
    }

    floyd(a, n);

    printf("\nShortest path matrix:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (a[i][j] == INF) {
                printf("INF ");
            } else {
                printf("%d   ", a[i][j]);
            }
        }
        printf("\n");
    }
    return 0;
}






9)



#include<stdio.h>
int w[10],p[10],n;
int max(int a,int b)
{
return a>b?a:b;
}
int knap(int i,int m)
{
if(i==n) return w[i]>m?0:p[i];
if(w[i]>m) return knap(i+1,m);
return max(knap(i+1,m),knap(i+1,m-w[i])+p[i]);
}
int main()
{
int m,i,max_profit;
printf("\nEnter the no. of objects:");
scanf("%d",&n);
printf("\nEnter the knapsack capacity:");
scanf("%d",&m);
printf("\nEnter profit followed by weight:\n");
for(i=1;i<=n;i++)
scanf("%d %d",&p[i],&w[i]);
max_profit=knap(1,m);
printf("\nMax profit=%d",max_profit);
return 0;
}






10 a) prims




#include <stdio.h>

#define INF 999
#define MAX 10

void prims(int cost[MAX][MAX], int n) {
    int visited[MAX] = {0};
    int mincost = 0, num_edges = 0;

    visited[0] = 1; // Start from the first vertex
    printf("\nEdges of the Minimum Spanning Tree (Prim's):\n");

    while (num_edges < n - 1) {
        int min = INF, u = -1, v = -1;

        // Find the absolute minimum weight edge connecting visited to unvisited nodes
        for (int i = 0; i < n; i++) {
            if (visited[i]) {
                for (int j = 0; j < n; j++) {
                    if (!visited[j] && cost[i][j] < min) {
                        min = cost[i][j];
                        u = i;
                        v = j;
                    }
                }
            }
        }

        // Add the valid edge to the tree
        if (u != -1 && v != -1) {
            printf("Edge (%d, %d) = %d\n", u, v, min);
            mincost += min;
            visited[v] = 1;
            num_edges++;
        }
    }
    printf("Minimum Total Cost (Prim's) = %d\n", mincost);
}

int main() {
    int n, cost[MAX][MAX];

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    printf("Enter the cost adjacency matrix (use 999 for no edge, 0 for self loops):\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &cost[i][j]);
            if (cost[i][j] == 0 && i != j) {
                cost[i][j] = INF; // Convert 0s to INF for correct evaluation
            }
        }
    }

    prims(cost, n);
    return 0;
}





10b ) Kruskal




#include<stdio.h> 
#define INFINITY 999 
#define MAX 10 

struct EDGE { 
    int x, y, wt; 
} e[MAX]; 

int parent[MAX]; 
int cost[MAX][MAX]; 
int t[MAX][2]; 
int nedges; 
int eno; 

void sort_edges() { 
    int i, j; 
    struct EDGE temp; 
    for(i = 1; i < nedges; i++) {
        for(j = 1; j < nedges - i; j++) {
            if(e[j].wt > e[j + 1].wt) { 
                temp = e[j]; 
                e[j] = e[j + 1]; 
                e[j + 1] = temp; 
            } 
        }
    }
} 

int get_parent(int v) { 
    while(parent[v]) {
        v = parent[v]; 
    }
    return v; 
} 

void join(int i, int j) { 
    parent[j] = i; 
} 

void kruskal(int n) { 
    int i, j, k, sum = 0; 
    int eno = 1; 
    struct EDGE nextedge; 
    
    for(k = 1; k < n; ) { 
        nextedge = e[eno++]; 
        i = get_parent(nextedge.x); 
        j = get_parent(nextedge.y); 
        if(i != j) { 
            join(nextedge.x, j); 
            t[k][1] = nextedge.x; 
            t[k][2] = nextedge.y; 
            sum = sum + nextedge.wt; 
            k++; 
        } 
    } 
    
    printf("\nCost of the spanning tree is: %d\n", sum); 
    printf("\nThe edges of the spanning tree are:\n"); 
    for(i = 1; i < n; i++) {
        printf("%d -> %d\n", t[i][1], t[i][2]); 
    }
} 

int main() { 
    int i, j; 
    int n; 
    
    printf("\nEnter the no.of vertices: "); 
    scanf("%d", &n); 
    
    for(i = 1; i <= n; i++) {
        parent[i] = 0; 
    }
    
    eno = 1; 
    printf("\nEnter the cost adjacency matrix: 0 = self loop & 999 = no edge\n"); 
    for(i = 1; i <= n; i++) { 
        for(j = 1; j <= n; j++) { 
            scanf("%d", &cost[i][j]); 
            if(i == j || cost[i][j] == INFINITY) {
                continue; 
            }
            e[eno].x = i; 
            e[eno].y = j; 
            e[eno].wt = cost[i][j]; 
            eno++; 
            nedges++; 
        } 
    } 
    
    sort_edges(); 
    kruskal(n);
    return 0;
}






11) 


#include <stdio.h>
#include <stdlib.h>
#define INFINITY 999

void dijkstra(int cost[10][10], int n, int source, int v[10], int d[10]) 
{
    int min, i, j, u;
    v[source] = 1;
    for (i = 1; i <= n; i++) 
    {
        min = INFINITY;
        for (j = 1; j <= n; j++) 
        {
            if (v[j] == 0 && d[j] < min) 
            {
                min = d[j];
                u = j;
            }
        }
        v[u] = 1;
        for (j = 1; j <= n; j++) 
        {
            if (v[j] == 0 && (d[j] > (d[u] + cost[u][j]))) 
            {
                d[j] = d[u] + cost[u][j];
            }
        }
    }
}

int main() 
{
    int n, cost[10][10], sourceNode, v[10], d[10];
    int i, j;
    printf("Enter no of vertices: ");
    scanf("%d", &n);
    printf("Enter Cost Adjacency matrix:\n");
    for (i = 1; i <= n; i++) 
    {
        for (j = 1; j <= n; j++) 
        {
            scanf("%d", &cost[i][j]);
        }
    }
    printf("Enter the source (%d to %d):\n", 1, n);
    scanf("%d", &sourceNode);
    for (i = 1; i <= n; i++) 
    {
        d[i] = cost[sourceNode][i];
        v[i] = 0;
    }
    
    dijkstra(cost, n, sourceNode, v, d);
    
    printf("Shortest distance from %d\n", sourceNode);
    for (i = 1; i <= n; i++) 
    {
        printf("%d -> %d = %d\n", sourceNode, i, d[i]);
    }
    return 0;
}









12)


#include<stdio.h>
#include<stdlib.h>
int x[10];
static int c=1;
void printBoard(int n)
{
    int i,j;
    printf("Solution %d:\n",c++);
    for(i=1;i<=n;i++)
    {
        for(j=1;j<=n;j++)
        {
            if(x[i]==j)
                printf("Q ");
            else
                printf("- ");
        }
        printf("\n");
    }
}
int place(int k, int i)
{
    int j;
    for(j=1;j<=k-1;j++)
    {
        if(x[j]==i || abs(x[j]-i)==abs(j-k))
            return 0;
    }
    return 1;
}
void nQueens(int k, int n)
{
    int i,j;
    for(i=1;i<=n;i++)
    {
        if(place(k,i))
        {
            x[k]=i;
            if(k==n)
            {
                printf("\n");
                printBoard(n);
            }
            else
                nQueens(k+1,n);
        }
    }
}
int main()
{
    int n;
    printf("Enter the number of queens:\n");
    scanf("%d",&n);
    nQueens(1,n);
    if(c==1)
        printf("No solutions");
    return 0;
}












| Program   | Algorithm                  | Best Case                      | Average Case   | Worst Case     |
| --------- | -------------------------- | ------------------------------ | -------------- | -------------- |
| **1(a)**  | Naive String Matching      | **O(n)**                       | **O(nm)**      | **O(nm)**      |
| **1(b)**  | Iterative Binary Search    | **O(1)**                       | **O(log n)**   | **O(log n)**   |
| **2**     | Merge Sort                 | **O(n log n)**                 | **O(n log n)** | **O(n log n)** |
| **3**     | Quick Sort                 | **O(n log n)**                 | **O(n log n)** | **O(n²)**      |
| **4(a)**  | Depth First Search (DFS)   | **O(V²)** *(Adjacency Matrix)* | **O(V²)**      | **O(V²)**      |
| **4(b)**  | Breadth First Search (BFS) | **O(V²)** *(Adjacency Matrix)* | **O(V²)**      | **O(V²)**      |
| **5**     | Topological Sort (DFS)     | **O(V²)** *(Adjacency Matrix)* | **O(V²)**      | **O(V²)**      |
| **6**     | Horspool String Matching   | **O(n/m)**                     | **O(n)**       | **O(nm)**      |
| **7**     | Warshall's Algorithm       | **O(n³)**                      | **O(n³)**      | **O(n³)**      |
| **8**     | Floyd's Algorithm          | **O(n³)**                      | **O(n³)**      | **O(n³)**      |
| **9**     | 0/1 Knapsack (Recursive)   | **O(2ⁿ)**                      | **O(2ⁿ)**      | **O(2ⁿ)**      |
| **10(a)** | Prim's Algorithm           | **O(V²)** *(Adjacency Matrix)* | **O(V²)**      | **O(V²)**      |
| **10(b)** | Kruskal's Algorithm        | **O(E log E)**                 | **O(E log E)** | **O(E log E)** |
| **11**    | Dijkstra's Algorithm       | **O(V²)** *(Adjacency Matrix)* | **O(V²)**      | **O(V²)**      |
| **12**    | N-Queens (Backtracking)    | **O(N!)**                      | **O(N!)**      | **O(N!)**      |

