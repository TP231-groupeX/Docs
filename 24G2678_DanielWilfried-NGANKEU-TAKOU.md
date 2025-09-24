Practical Work INF231 – 9 Exercises

**Student:** Ngankeu Takou Daniel Wilfried 
**Matricule:** 24G2678
**Course:** INF231
**Assignment:** 9 Exercises - Write C programs for the following tasks: 
**Date:** 24/09/2025 

Exercise Outline
1. [Exercise 1 – Sum of Two Matrices](#exercise-1)
2. [Exercise 2 – Multiply Two Matrices](#exercise-2)
3. [Exercise 3 – Sequential Search in an Array](#exercise-3)
4. [Exercise 4 – Multiply Two Numbers Using +1](#exercise-4)
5. [Exercise 5 – Test if an Array is Sorted](#exercise-5)
6. [Exercise 6 – Median of an Array](#exercise-6)
7. [Exercise 7 – Invert an Array](#exercise-7)
8. [Exercise 8 – Vector Product](#exercise-8)
9. [Exercise 9 – Vector × Matrix Product](#exercise-9)

## Exercise 1 – Sum of Two Matrices

**Problem Statement** 
Write a program to read two matrices **A** and **B** of the same dimensions and compute their sum matrix **C**.

**Algorithm (Pseudocode)** 
Read n (rows) and p (columns)

Read elements of matrix A

Read elements of matrix B

Initialize C as an empty matrix of size n x p

For i from 0 to n-1
For j from 0 to p-1
C[i][j] = A[i][j] + B[i][j]

Print matrix C

**Implementation (C)**
#include <stdio.h>

int main() {
    int n, p;
    printf("Enter dimensions of matrices (rows cols): ");
    scanf("%d %d", &n, &p);

    double A[n][p], B[n][p], C[n][p];

    printf("Enter elements of matrix A:\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < p; j++)
            scanf("%lf", &A[i][j]);

    printf("Enter elements of matrix B:\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < p; j++)
            scanf("%lf", &B[i][j]);

    for (int i = 0; i < n; i++)
        for (int j = 0; j < p; j++)
            C[i][j] = A[i][j] + B[i][j];

    printf("Result matrix C:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < p; j++)
            printf("%8.2lf ", C[i][j]);
        printf("\n");
    }

    return 0;
}
Time Complexity: O(n × p)
Sample Input / Output
Input:
2 2
1 2
3 4
5 6
7 8

Output:
6.00  8.00
10.00 12.00
Exercise 2 – Multiply Two Matrices
Problem Statement
Compute the product of two matrices A (n×p) and B (p×m) to get C (n×m).

Algorithm (Pseudocode)
1. Read n, p, m
2. Read matrix A (n x p)
3. Read matrix B (p x m)
4. Initialize matrix C with zeros
5. For i in 0..n-1
       For j in 0..m-1
           For k in 0..p-1
               C[i][j] += A[i][k] * B[k][j]
6. Print matrix C

Implementation (C):
#include <stdio.h>

int main() {
    int n, p, m;
    printf("Enter dimensions of matrix A (rows cols): ");
    scanf("%d %d", &n, &p);
    printf("Enter number of columns of matrix B: ");
    scanf("%d", &m);

    double A[n][p], B[p][m], C[n][m];

    printf("Enter elements of matrix A:\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < p; j++)
            scanf("%lf", &A[i][j]);

    printf("Enter elements of matrix B:\n");
    for (int i = 0; i < p; i++)
        for (int j = 0; j < m; j++)
            scanf("%lf", &B[i][j]);

    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            C[i][j] = 0.0;

    for (int i = 0; i < n; i++)
        for (int k = 0; k < p; k++)
            for (int j = 0; j < m; j++)
                C[i][j] += A[i][k] * B[k][j];

    printf("Result matrix C:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++)
            printf("%8.0lf ", C[i][j]);
        printf("\n");
    }
    return 0;
}
Time Complexity: O(n × p × m)

**Sample Input / Output**
Input:
2 3
1 2 3
4 5 6
3
7 8 9
10 11 12
13 14 15

Output:
66 72 78
156 171 186

Exercise 3 – Sequential Search in an Array
Problem Statement
Search for an element in an array using sequential search.

Time Complexity: O(n)

Implementation (C)

#include <stdio.h>
#include <stdlib.h>

int sequentialSearch(int arr[], int size, int target){
    for(int i = 0; i < size; i++)
        if(arr[i] == target) return i;
    return -1;
}

int main() {
    int size, target;
    printf("Enter size of array: ");
    scanf("%d", &size);
    int arr[size];
    for(int i = 0; i < size; i++){
        printf("Enter element %d: ", i+1);
        scanf("%d", &arr[i]);
    }
    printf("Enter element to search: ");
    scanf("%d", &target);
    int result = sequentialSearch(arr, size, target);
    if(result != -1) printf("%d found at position %d\n", target, result);
    else printf("Element not found\n");
    return 0;
}
**Sample Input / Output**

Input: 5, elements: 1 3 5 7 9, target 5
Output: 5 found at position 2

**Exercise 4 – Multiply Two Numbers Using +1**
Problem Statement
Compute a × b using only the +1 operator.

Time Complexity: O(a × b)

Implementation (C)
#include <stdio.h>

int add(int x, int y){
    int sum = x;
    for(int i = 0; i < y; i++)
        sum = sum + 1;
    return sum;
}

int multiply(int a, int b){
    int result = 0;
    for(int i = 0; i < b; i++)
        result = add(result, a);
    return result;
}

int main(){
    int a, b;
    printf("Enter a and b: ");
    scanf("%d %d", &a, &b);
    printf("%d * %d = %d\n", a, b, multiply(a, b));
    return 0;
}
Sample Input / Output

Input:
Enter a and b: 4 3
Output:
4 * 3 = 12

Exercise 5 – Test if an Array is Sorted
Problem Statement
Check if an array is sorted in ascending order.

Time Complexity: O(n)

Implementation (C)
#include <stdio.h>

void sortTest(int arr[], int size){
    for(int i = 0; i < size - 1; i++)
        if(arr[i] > arr[i+1]){
            printf("Array not sorted\n");
            return;
        }
    printf("Array is sorted\n");
}

int main(){
    int size;
    printf("Enter size of array: ");
    scanf("%d", &size);
    int arr[size];
    for(int i = 0; i < size; i++){
        printf("Enter element %d: ", i+1);
        scanf("%d", &arr[i]);
    }
    sortTest(arr, size);
    return 0;
}

Sample Input / Output

Input:
Enter size of array: 5
Enter elements: 1 3 5 7 9
Output:
Array is sorted

Exercise 6 – Median of an Array
Problem Statement
Compute the median of a sorted array.

Time Complexity: O(n) (for validation)

Implementation (C)
#include <stdio.h>

double median(int arr[], int size){
    for(int i = 0; i < size - 1; i++)
        if(arr[i] > arr[i+1]){
            printf("Array not sorted\n");
            return -1;
        }
    if(size % 2 == 1) return arr[size/2];
    else return (arr[size/2 - 1] + arr[size/2]) / 2.0;
}

int main(){
    int size;
    printf("Enter size of array: ");
    scanf("%d", &size);
    int arr[size];
    printf("Enter elements: ");
    for(int i = 0; i < size; i++) scanf("%d", &arr[i]);
    printf("Median = %.2f\n", median(arr, size));
    return 0;
}

Sample Input / Output

Input:
Enter size of array: 5
Enter elements: 1 3 5 7 9
Output:
Median = 5.00

Input:
Enter size of array: 6
Enter elements: 2 4 6 8 10 12
Output:
Median = 7.00

Exercise 7 – Invert an Array
Problem Statement
Reverse the elements of an array in place.

Time Complexity: O(n)

Implementation (C)
#include <stdio.h>

void invertArray(int arr[], int size){
    int start = 0, end = size - 1;
    while(start < end){
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++; end--;
    }
}

int main(){
    int size;
    printf("Enter size of array: ");
    scanf("%d", &size);
    int arr[size];
    for(int i = 0; i < size; i++){
        printf("Enter element %d: ", i+1);
        scanf("%d", &arr[i]);
    }
    invertArray(arr, size);
    for(int i = 0; i < size; i++) printf("%d ", arr[i]);
    printf("\n");
    return 0;
}

Sample Input / Output

Input:
Enter size of array: 5
Enter elements: 1 2 3 4 5
Output:
5 4 3 2 1

Input:
Enter size of array: 3
Enter elements: 7 8 9
Output:
9 8 7

Exercise 8 – Vector Product
Problem Statement
Compute the cross product of two 3D vectors.

Time Complexity: O(1)

Implementation (C)
#include <stdio.h>

int main(){
    int u[3], v[3], w[3];
    printf("Enter vector u: ");
    for(int i=0;i<3;i++) scanf("%d",&u[i]);
    printf("Enter vector v: ");
    for(int i=0;i<3;i++) scanf("%d",&v[i]);

    w[0] = u[1]*v[2] - u[2]*v[1];
    w[1] = u[2]*v[0] - u[0]*v[2];
    w[2] = u[0]*v[1] - u[1]*v[0];

    printf("Cross product: [%d, %d, %d]\n", w[0], w[1], w[2]);
    return 0;
}

Input:
Enter vector u: 1 2 3
Enter vector v: 4 5 6
Output:
Cross product: [-3, 6, -3]

Input:
Enter vector u: 2 0 1
Enter vector v: 1 3 2
Output:
Cross product: [-3, 0, 6]

Exercise 9 – Vector × Matrix Product
Problem Statement
Multiply a vector by a matrix (vector as row, matrix n×m) to get a resulting vector.

Time Complexity: O(n × m)

Implementation (C)
#include <stdio.h>

int main(){
    int n, m;
    printf("Enter size of vector and columns of matrix: ");
    scanf("%d %d", &n, &m);
    int v[n], M[n][m], p[m];
    printf("Enter elements of vector:\n");
    for(int i=0;i<n;i++) scanf("%d",&v[i]);
    printf("Enter elements of matrix:\n");
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            scanf("%d",&M[i][j]);
            }
           } 
    for(int j=0;j<m;j++){
        p[j]=0;
        for(int i=0;i<n;i++)
            p[j]+=v[i]*M[i][j];
    }
    printf("Resulting vector: ");
    for(int j=0;j<m;j++) printf("%d ",p[j]);
    printf("\n");
    return 0;
}

Input:
Enter size of vector and columns of matrix: 2 3
Enter elements of vector: 1 2
Enter elements of matrix:
1 2 3
4 5 6
Output:
Resulting vector: 9 12 15

Input:
Enter size of vector and columns of matrix: 3 2
Enter elements of vector: 2 0 1
Enter elements of matrix:
1 2
3 4
5 6
Output:
Resulting vector: 7 10
