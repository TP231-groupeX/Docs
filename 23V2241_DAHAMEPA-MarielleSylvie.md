# Matrix Multiplication in C — Documentation

## Project Overview

This project demonstrates the multiplication of two matrices using a simple, nested-loop algorithm and implements it in C. It allows the user to input two matrices of compatible dimensions and outputs their product.

## Problem Statement

Given two matrices A and B, compute the product C = A × B, where:

- Multiplication is possible only if the number of columns in A equals the number of rows in B (cols_A == rows_B).
- The resulting matrix C has dimensions (rows_A × cols_B).

## Principle

### Compatibility Condition
Matrix multiplication is valid only if:
```
columns of A == rows of B
```

### Resulting Matrix Size
If A is of size (m × n) and B is of size (n × p), then C will be of size (m × p).

### Computation
Each element C[i][j] is computed as:
```
C[i][j] = Σ (A[i][k] * B[k][j]) for k = 0 to n-1
```

## Data Dictionary

| Variable | Type | Description |
|----------|------|-------------|
| `matrixA[MAX][MAX]` | int | First input matrix |
| `matrixB[MAX][MAX]` | int | Second input matrix |
| `matrixC[MAX][MAX]` | int | Resultant product matrix |
| `rowA, columnA` | int | Dimensions of matrix A |
| `rowB, columnB` | int | Dimensions of matrix B |
| `i, j, k` | int | Loop indices |

## Algorithm Steps

1. Read matrix sizes and validate that dimensions are positive integers within the maximum allowed size.
2. Check compatibility: Ensure columns of A == rows of B.
3. Input matrix elements for both matrices.
4. Verify number of elements matches the declared size.
5. Multiply matrices using nested loops:
   ```
   for i = 0 to rowA-1
       for j = 0 to columnB-1
           matrixC[i][j] = 0
           for k = 0 to columnA-1
               matrixC[i][j] += matrixA[i][k] * matrixB[k][j]
   ```
6. Display the resulting matrix C.

## Usage

**Compile the C program:**
```bash
gcc matrix_multiplication.c -o matrix_multiplication
```

**Run the executable:**
```bash
./matrix_multiplication
```

**Follow prompts to enter:**
- Dimensions of matrices A and B
- Elements of matrices A and B
- View the resulting matrix C

## Example Run

```
Enter number of rows for Matrix A: 2
Enter number of columns for Matrix A: 3
Enter number of rows for Matrix B: 3
Enter number of columns for Matrix B: 2

Enter elements of Matrix A:
1 2 3
4 5 6

Enter elements of Matrix B:
7 8
9 10
11 12

Product of matrices is:
58 64
139 154
```

## Implementation Details

- **Language:** C
- **Maximum matrix size:** 100 × 100
- Input validation ensures sizes are positive integers and do not exceed maximum allowed dimensions.
- Element count verification ensures user enters the correct number of elements.
- **Key function:** `ReadMatrixSize()` handles size input and validation for each matrix.

### Multiplication Logic
```c
for (int i = 0; i < rowA; i++) {
    for (int j = 0; j < columnB; j++) {
        matrixC[i][j] = 0;
        for (int k = 0; k < columnA; k++) {
            matrixC[i][j] += matrixA[i][k] * matrixB[k][j];
        }
    }
}
```

## Time and Space Complexity

### Time Complexity

Matrix multiplication requires iterating over all elements of the resulting matrix and performing a sum of products for each element.

For matrices of size A(m × n) and B(n × p):

**Time Complexity:** O(m × n × p)

**Explanation:**
- Outer loop → m iterations (rows of A)
- Middle loop → p iterations (columns of B)
- Inner loop → n iterations (columns of A / rows of B)

### Space Complexity

Uses three matrices of size MAX × MAX regardless of input size:

**Space Complexity:** O(MAX²)

If considering only required space based on input sizes:

**Space Complexity:** O(m × n + n × p + m × p)

Auxiliary variables i, j, k contribute O(1).

## Notes

- Ensure matrices are compatible; otherwise, multiplication is impossible.
- Current implementation uses static array sizes (MAX = 100). Dynamic memory allocation can be used for larger matrices.
- Validates element count for safety to prevent mismatched input.








# Sequential Search in an Array

## Problem

The task is to search for a specific value in an array of integers using the sequential (linear) search method.

## Principle

Sequential search is a simple searching technique where each element of the array is compared with the target value in order, starting from the first element. The search stops either when the value is found or when all elements have been checked.

## Data Dictionary

| Variable | Type | Description |
|----------|------|-------------|
| `arr[100]` | `int` array | Stores the elements of the array (maximum 100 elements) |
| `n` | `int` | Number of elements in the array |
| `i` | `int` | Loop index for traversing the array |
| `value_to_search` | `int` | Value to be searched in the array |
| `found` | `bool` | Flag indicating whether the value was found |

## Algorithm

```plaintext
Algorithm: SequentialSearch
Variables:
    arr[100] : integers
    n, i, value_to_search : integer          
    found : boolean

Start
    // Read size of array
    Write("Enter number of elements (≤ 100): ")
    Read n
    While (n < 1 OR n > 100)
        Write("Enter a valid positive integer ≤ 100: ")
        Read n
    End While
    
    // Read elements of array
    Write("Enter elements of the array:")
    For i <- 0 TO n-1
        Read arr[i]
    End For
    
    // Read value to search
    Write("Enter value to search: ")
    Read value_to_search
    
    // Perform the search
    found <- false
    For i <- 0 TO n-1
        If arr[i] = value_to_search Then
            Write("Value found at position ", i)
            found <- true
            Break
        End If
    End For
    
    // If not found
    If found = false Then
        Write("Value not found in array")
    End If
End
```

## Example

Suppose the array contains:
```
arr = [12, 45, 23, 67, 34]
n = 5
value_to_search = 67
```

**Step-by-step search:**
1. Compare arr[0] (12) with 67 → not equal
2. Compare arr[1] (45) with 67 → not equal
3. Compare arr[2] (23) with 67 → not equal
4. Compare arr[3] (67) with 67 → equal

**Result:**
```
Value found at position 3
```

If `value_to_search = 99`, the algorithm checks all elements and outputs:
```
Value not found in array
```

## Implementation in C

```c
#include <stdio.h>
#include <stdbool.h>   
#define MAX_SIZE 100

int main() {
    int arr[MAX_SIZE];
    int n, i, value_to_search;
    bool found = false;
    
    // Read size of the array
    printf("Enter number of elements (≤ 100): ");
    scanf("%d", &n);
    while (n < 1 || n > MAX_SIZE) {
        printf("Enter a valid positive integer ≤ 100: ");
        scanf("%d", &n);
    }
    
    // Read elements of the array
    printf("Enter elements of the array:\n");
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    // Read value to search
    printf("Enter value to search: ");
    scanf("%d", &value_to_search);
    
    // Perform the search
    for (i = 0; i < n; i++) {
        if (arr[i] == value_to_search) {
            printf("Value found at position %d\n", i);
            found = true;
            break;
        }
    }
    
    if (!found) {
        printf("Value not found in array\n");
    }
    
    return 0;
}
```

## Time Complexity

- **Best Case:** O(1) – when the value is found at the first position
- **Worst Case:** O(n) – when the value is at the last position or not present
- **Average Case:** O(n) – the value is found after checking half of the elements on average

## Space Complexity

**O(1)** – only a constant amount of extra memory is used for variables, regardless of the array size.
