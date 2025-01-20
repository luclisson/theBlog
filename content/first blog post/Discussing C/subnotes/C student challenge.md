
---

### Task: **Number Operations**

Write a program that performs the following:

1. Accept a list of integers from the user (maximum size 100).
2. Allow the user to perform multiple operations:
    - **Find the smallest number.**
    - **Find the largest number.**
    - **Sort the numbers in ascending or descending order.**
    - **Find the sum and average of the numbers.**
3. Implement each operation as a function for better modularity.
4. Measure the time taken for each operation and display it.

---

### Requirements:

- Use standard I/O functions for input and output.
- Allow users to repeatedly choose operations until they decide to exit.
- Include input validation to handle incorrect inputs gracefully.
- Use a header file to define constants or reusable functions (optional for modularity).

---

### Example Run:

```plaintext
Enter the number of integers (max 100): 6
Enter 6 integers: 5 2 9 1 4 3

Choose an operation:
1. Find Smallest
2. Find Largest
3. Sort (Ascending)
4. Sort (Descending)
5. Sum and Average
6. Exit

Enter your choice: 3
Sorted numbers (Ascending): 1 2 3 4 5 9
Operation took 0.000032 seconds.

Choose an operation:
5
Sum: 24, Average: 4.00
Operation took 0.000012 seconds.

Enter your choice: 6
Goodbye!
```

---
[[sample solution(ChatGPT)]]