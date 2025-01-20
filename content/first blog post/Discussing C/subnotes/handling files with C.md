
- to handle a file in c, first you need to declare a pointer var of the type FILE
- use the fopen(filename, mode) function to work with the file
- modes:
  1. w - wirte
  2. a - append
  3. r - read
- if the file doesn't exist the program creates one for you
- you can pass an exact file path as filename if the file isn't part of you programming project
- when you're finished working with the file, you have to close it using the fclose(pointer_name) function
	-why do I have to close the file
		1. saving your changes
		2. let other programs open the file
		3. clean up memory space
- important function when working with files:
	1. fprintf(pointer, "");
	2. fgets(var, int, pointer)
	   - var should be the var name of your variable you want to assing the files content to
	   - int is the required maximum size of data to be read
	3. fgets() only reads the first line of the files content
	   --> code a loop which reads all of the file e.g. a while loop
	   note that fgets() returns a success value


