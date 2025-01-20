### memory management 

**vocab when managing memory**
- allocation= reserving memory
- reallocating= reserves a different size of memory for an already allocated memory block
- deallocate memory= also referred as freeing memory
- be aware that its possible to damage data which is stored in other memory addresses if you handle a pointer falsely

#### different types of memory
- static memory: memory which is reserved for variables before the program runs (happens when the program is compiled)
- problem with static memory:
  if you define an array with x amount of elements and end up not using the entire space, you're wasting memory space and the program could run faster.
- dynamic memory: memory is allocated after the program is compiled
- solution to the static memory problem using dynamic memory:
  use memory on demand using `malloc()`, `calloc()`, or `realloc()`
  you can manually free memory using free() --> note that the free() method erases all of the allocated memory and not only the unused
  ```c
  int *ptr = malloc(10*sizeof(int));
  if (ptr != NULL){
  ptr[0]=1;
  }
  //imagine some other program code
  free(ptr); // free all the allocated memory when you don't need it anymore
  ptr = NULL; // avoid accessing a dangling pointer
  
```
**What is a dangling pointer**
- when you free the pointer after using the free() method, the pointer still holds the memory address. The address isn't valid anymore, this can lead to undefined behaviour or even lead to the program crashing.

**What is the difference between malloc, calloc and realloc?
	- malloc:
		- allocates a single block of a specific size
		- single contiguous block
		- memory content is uninitialized
		- return a pointer (if it fails it returns NULL)
	- calloc:
		- allocates memory for an array of elements
		- all bytes are initialized to zero
		- allocates contiguous block for multiple elements
		- returns a pointer (if it fails it returns NULL)
	- realloc (used to reallocate memory):
		- resizes a allocated memory block (increase or decrease)
		- if size is increased, the new allocated memory is not initialized
		- if the size is decreased, the memory is also freed
		- it may changes the memory address
		- returns a pointer (if it fails it returns NULL)
		- if null is returned, the original memory block remains untouched

different syntax examples:

```c
//malloc
int *ptr = malloc(5 * sizeof(int));  // Allocates memory
if (ptr != NULL) {
    ptr[0] = 10;  //initialize values
}
//calloc
int *ptr = calloc(5, sizeof(int));  // Allocates and initializes memory to 0
if (ptr != NULL) {
    printf("%d\n", ptr[0]);  // Outputs 0 (initialized to zero)
}
//realloc
int *ptr = malloc(5 * sizeof(int));  // Allocates memory block
if (ptr != NULL) {
    ptr = realloc(ptr, 10 * sizeof(int));  // Resizes the block
    if (ptr != NULL) {
        ptr[5] = 42;  // New memory can be used; 5 is part of the new allocated                           memory, because it's the 6th int
    }
}
```

- stack memory- how does memory management of functions work?
	- when vars inside of functions are defined they use stack memory rather than static memory. When the function return a stack the allocated memory is freed again.