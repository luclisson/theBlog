I will safe all of my written notes in the this file

- After one time the selected pivot is in it's final position
- 2 requirement to be at the right position:
	1. all items left are greater
	2. all items right are smaller

How to select the first pivot?
- 1st element
- last element
- random element
- median of three method
  1. select first, last and middle element
  2. sort them
  3. middle one is the first pivot
	- we assume that this value is somewhat close to the actual value which should be in the middle to equal out the work on each sub partition 

Algoritm 
1. 2 6 5 <mark style="background: #FFB86CA6;">3</mark> 8 7 1 0 for this example we will assume 3 is our pivot
2. change pivot with the last entity
   2 6 5 <mark style="background: #FFB86CA6;">0</mark> 8 7 1 <mark style="background: #FFB86CA6;">3</mark>
3. search for two items
   - item from the left (first one which is greater than pivot)
   - item form the right (first one which is smaller than pivot)
	2 <mark style="background: #FFB86CA6;">6</mark> 5 0 8 7 <mark style="background: #FFB86CA6;">1</mark> 3
	- swap the two
	2 <mark style="background: #FFB86CA6;">1</mark> 5 0 8 7 <mark style="background: #FFB86CA6;">6</mark> 3
4. repeat this step until the index of the left item is greater than the index of the right item. If this happens, swap the left item with the pivot --> pivot is now at it's final position
	2 1 <mark style="background: #FFB86CA6;">5</mark> <mark style="background: #FFB86CA6;">0</mark> 8 7 6 3
	--> 2 1 <mark style="background: #FFB86CA6;">0</mark> <mark style="background: #FFB86CA6;">5</mark> 8 7 6 3
	now the left item's index is 3 and the right item's index is 
5. swap the left item with the pivot
	2 1 0 <mark style="background: #FFB86CA6;">3</mark> 8 7 6 <mark style="background: #FFB86CA6;">5</mark> 
	3 (the original pivot is now at it's final position)

How to choose the next pivot?
- quicksort is recursive which means it repeats itself by calling it's function on its own
- divide the original array into 2 partitions
  1. all elements which are smaller than pivot
  2. all elements which are greater than pivot
- repeat the same process until every partition only has 0 or 1 element
Why do I not have to put the partitions back together?
- I can work with pointer and memory addresses and change the positions on the memory. Thats why I don't have to return any values

your array should now be sorted

speed: (something with big O and log)