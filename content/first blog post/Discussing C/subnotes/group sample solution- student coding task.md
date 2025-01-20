Paste the group solution of the [[C student challenge]]

```c
#include <stdio.h>
#include <stdlib.h>

void printArr(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int medianThree(int arr[], int* low, int* high) {
    int mid = *low + (*high - *low) / 2;

    if (arr[*low] > arr[mid]) {
        swap(&arr[*low], &arr[mid]);
    }
    if (arr[mid] > arr[*high]) {
        swap(&arr[mid], &arr[*high]);
    }
    if (arr[*low] > arr[mid]) {
        swap(&arr[*low], &arr[mid]);
    }

    return arr[mid];
}

int pivotFinalPos(int arr[], int start, int end, int pivot) {
    int left = start;
    int right = end;

    while (left < right) {
        while (arr[left] < pivot) {
            left++;
        }
        while (arr[right] > pivot) {
            right--;
        }
        if (left <= right) {
            swap(&arr[left], &arr[right]);
            left++;
            right--;
        }
    }
    return left;
}

int quickSort(int arr[], int start, int end) {
    if (start >= end) return 0;

    int pivot = medianThree(arr, &start, &end);
    int pivotIndex = pivotFinalPos(arr, start, end, pivot);

    quickSort(arr, start, pivotIndex - 1); // Recursively sort the left partition
    quickSort(arr, pivotIndex, end);       // Recursively sort the right partition
    return 0;
}

int sortAscending(int arr[], int size) {
    printArr(arr, size);
    quickSort(arr, 0, size - 1);
    printArr(arr, size);
    return 0;
}

int findSmallest(int arr[], int size){
    int smallest = 32767; //highest integer value possible
    for(int i = 0; i<size; i++){
        if (arr[i] < smallest){
            smallest = arr[i];
        }
    }
    return smallest;
}
int findHighest(int arr[], int size){
    int highest = 0;
    for(int i = 0; i<size; i++){
        if(arr[i]> highest){
            highest= arr[i];
        }
    }
    return highest;
}
float calcAverage(int arr[], int size){
    int num = 0;
    for(int i = 0; i<size; i++){
        num = num + arr[i];
    }
    return num/size;
}
int calcSum(int arr[], int size){
    int sum = 0;
    for(int i = 0; i<size; i++){
        sum = sum + arr[i];
    }
    return sum;
}
int displayInterface (){
    int size;
    printf("Enter the number of integers (max 100):");
    scanf("%d", &size);
    int* arr = (int*)malloc(size * sizeof(int));
    if (arr == NULL){
        printf("Memory allocation failed");
        return 1;
    }
    printf("Enter %d intergers: ", size);
    for(int i = 0; i<size; i++){
        
        scanf(" %d", &arr[i]);
    }
    printf("you entered: ");
    printArr(arr, size);
    printf("\n\nChose an operation:\n1. Find the smallest\n2. Find largeset\n3. Sort Ascending\n4. Sum\n5. Average\n6. Exit\n");
    int choice;
    scanf("%d", &choice);
    switch(choice){
        case 1:
            printf("The smallest number is: %d\n", findSmallest(arr, size));
            break;
        case 2:
            printf("The largest number is: %d\n", findHighest(arr, size));
            break;
        case 3:
            sortAscending(arr, size);
            break;
        case 4:
            printf("The sum of the numbers is: %d\n", calcSum(arr, size));
            break;
        case 5:
            printf("The average of the numbers is: %f\n", calcAverage(arr, size));
            break;
        case 6:
            return 0;
        default:
            printf("Invalid choice\n");
            break;
    }
    return 0;    
} 


int main() {
    displayInterface();
    return 0;
}
```