
this note will explain the binary search algorithm which searches for a specific entity in a sorted list

The binary search algorithm is a searching algorithm used in sorted arrays. It repeatedly divides the array in half to avoid looping through the entire array one by one.
You can use the binary search algorithm to return the index of the to be searched item or simply return of it exists in list or not.

### Conditions
- data must be sorted
- you must have access to all of the elements of the array

### How does it work?
- you divide the original array in half and compare the middle element to your number
- if its greater your new value range is from middle to the end and you again compare the middle element from your new range to your number
- same if the middle element is smaller than your number. The only difference is that your value range is now from the beginning to the middle
- repeat this process until end minus beginning is 1 or less. if this condition is true and you haven't found your number you can't form another valid middle value and haven't found your value which means your number is not included in the array
	- alternative condition:
	  start<=end
	  the condition ensures that the loop will initialize even with one 1 item. Start would be 0 and end would be 0 as well. The condition would be true and the program would enter the while loop. The value of start or low will be adjusted if the last element is not your to be searched num. After that start will be greater than end because mid will be 0 (mid=0 + (0-0)/2) and either the start var will 1 or the end var will be -1. This will exit the while loop and end the entire search algorithm to return -1 if the num wasn't found
### example code

```c
int binarySearch(int arr[], int num, int start, int end){
    //check if num is middle element of arr
    int mid = start + (end - start) / 2;
    if(num == arr[mid]) return mid; // shortest solution

    while(start<=end){
        int mid = start + (end - start) / 2;
        if(num == arr[mid]) return mid; // shortest solution

        if(arr[mid]<num){
            start = mid +1;
        }else{
            end = mid - 1;
        }
    }
    return -1;
}
```
### time complexity
- Best Case: O(1)
- Average Case: O(log N)
- Worst Case: O(log N)


