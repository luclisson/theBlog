Here’s a C program implementation for the [[C student challenge]] that covers the basic C knowledge and adds the competitive programming speed aspect. It uses functions, arrays, loops, conditionals, and times the execution of each operation.

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define MAX_SIZE 100

// Function to find the smallest number
int findSmallest(int arr[], int n) {
    int smallest = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < smallest) {
            smallest = arr[i];
        }
    }
    return smallest;
}

// Function to find the largest number
int findLargest(int arr[], int n) {
    int largest = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    return largest;
}

// Function to sort the array in ascending order
void sortAscending(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}

// Function to sort the array in descending order
void sortDescending(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] < arr[j]) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}

// Function to calculate the sum of the array
int calculateSum(int arr[], int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    return sum;
}

// Function to calculate the average of the array
float calculateAverage(int sum, int n) {
    return (float)sum / n;
}

int main() {
    int n;
    int arr[MAX_SIZE];

    // Taking input for the array size and elements
    printf("Enter the number of integers (max %d): ", MAX_SIZE);
    scanf("%d", &n);

    if (n > MAX_SIZE || n <= 0) {
        printf("Invalid number of elements.\n");
        return 1;
    }

    printf("Enter %d integers: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int choice;
    clock_t start, end;
    double time_taken;

    // Menu for user operations
    do {
        printf("\nChoose an operation:\n");
        printf("1. Find Smallest\n");
        printf("2. Find Largest\n");
        printf("3. Sort (Ascending)\n");
        printf("4. Sort (Descending)\n");
        printf("5. Sum and Average\n");
        printf("6. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                start = clock();
                printf("Smallest number: %d\n", findSmallest(arr, n));
                end = clock();
                time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
                printf("Operation took %.6f seconds.\n", time_taken);
                break;

            case 2:
                start = clock();
                printf("Largest number: %d\n", findLargest(arr, n));
                end = clock();
                time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
                printf("Operation took %.6f seconds.\n", time_taken);
                break;

            case 3:
                start = clock();
                sortAscending(arr, n);
                printf("Sorted numbers (Ascending): ");
                for (int i = 0; i < n; i++) {
                    printf("%d ", arr[i]);
                }
                printf("\n");
                end = clock();
                time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
                printf("Operation took %.6f seconds.\n", time_taken);
                break;

            case 4:
                start = clock();
                sortDescending(arr, n);
                printf("Sorted numbers (Descending): ");
                for (int i = 0; i < n; i++) {
                    printf("%d ", arr[i]);
                }
                printf("\n");
                end = clock();
                time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
                printf("Operation took %.6f seconds.\n", time_taken);
                break;

            case 5:
                start = clock();
                int sum = calculateSum(arr, n);
                float avg = calculateAverage(sum, n);
                printf("Sum: %d, Average: %.2f\n", sum, avg);
                end = clock();
                time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
                printf("Operation took %.6f seconds.\n", time_taken);
                break;

            case 6:
                printf("Goodbye!\n");
                break;

            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 6);

    return 0;
}
```

### Explanation:

1. **Functions**: Each operation is implemented in its own function, such as `findSmallest`, `findLargest`, `sortAscending`, etc.
2. **Input**: The program takes input for the size of the array and the numbers within it.
3. **Operations**: The user can choose between different operations, and the program will output the result while timing the operation.
4. **Time Measurement**: `clock()` function is used to measure the time taken by each operation.
5. **Sorting**: The sorting is implemented using a simple bubble sort, but it could be optimized for competitive programming by using more advanced algorithms.

---

This program covers:

- Arrays and loops
- Functions for modularity
- Conditional statements
- Time measurement for performance

Let me know if you need further clarifications or modifications!