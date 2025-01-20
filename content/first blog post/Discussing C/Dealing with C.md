
This document will deal with basic knowledge about C. Why is C so popular? What are the benefits of using C? How does Memory management work in C? These are all questions which will be covered in this article. Note that this is barely scratching the surface of the language. If you want to dive deeper into C we provided some links.
All of the blue highlighted text is clickable and guides you through some concepts in more detail.

To get you started we got you covered with a [[Getting started]] program which shows you your first C program. Furthermore you will learn how to install a compiler and run code from either the terminal or an IDE.
# Syntax
### variables
The different [[C Variable types]] are all initialized according to the same pattern.
```c
// varType varName = value;

int num = 1;
char letter = a; 
```
### comments
- "//"
```c
//this is a comment
```

### printf() function
- output to console
- only strings
- doesn't print new line
What is `\n` exactly?

The newline character (`\n`) is called an **escape sequence**, and it forces the cursor to change its position to the beginning of the next line on the screen. This results in a new line.
Examples of other valid escape sequences are:

| Escape Sequence | NoDescription                       |
| --------------- | ----------------------------------- |
| `\t`            | Creates a horizontal tab            |
| `\\`            | Inserts a backslash character (`\`) |
| `\"`            | Inserts a double quote character    |

### conditional sentences 
```c
if (condition1) {  
  // block of code to be executed if condition1 is true
} else if (condition2) {  
  // block of code to be executed if the condition1 is false and condition2 is true  
} else {  
  // block of code to be executed if the condition1 is false and condition2 is false  
}
```
Shorthand if-statement
```c
variable = (condition) ? expressionTrue : expressionFalse;
```

### functions
- to create a function you need to declare it outside of the main function
- to_be_returned_value function_name() {}
```c
void createdFunction(){
	printf("this is my function");
}

int main(){
	createdFunction();
	return 0;
}
```
- inside the braces you can define parameters which can be used inside the function block code
- when calling a function you have to use the same amount of parameters you defined in the building process of the function, otherwise you will receive an error.
```c
void createdFunction(char a, int b){
	printf("my first parameter is %c\n", a);
	printf("my second parameter is %d", b);
}

int main(){
	createdFunction("L", 9);
}
```

When we're talking about function the concept of [[C scopes- a visualization]] is very important to be aware of. 
### switch-statement 
When do I use a switch statement?
If you have many if else statements a switch statement could be efficient to add readability.
```c
switch (expression) {  
  case x:  
    // code block  
    break;  
  case y:  
    // code block  
    break;  
  default:  
    // code block  
}
```

default block is optional and will be executed if no case matches.
DONT forget the break statement, else the next will be executed as well.
### while loop & for- loop
while loop:
```c
while (condition) {  
  // code block to be executed_  
}
```
for-loop:
```c
for (expression 1; expression 2; expression 3) {  
  // code block to be executed  
}
//example:

for (int i = 0; i < 5; i++) {  
  printf("%d\n", i);  
}
```
**Expression 1** is executed (one time) before the execution of the code block.

**Expression 2** defines the condition for executing the code block.

**Expression 3** is executed (every time) after the code block has been executed.
### arrays
```c
int myNumbers[] = {25,50,75,100}
```

- avoid mixing data types
- sizeof(arrayName) return the actual byte size of the variable which holds the defined array

```c
int myNumbers[] = {1,2,3,4};
int sizeArr = sizeof(myNumbers);
int sizeOfEl = sizeof(myNumbers[0]);
int lengthArr = sizeArr / sizeOfEl;

printf("%d\n", lengthArr);
```
### strings
- C doesn't have a String data type --> use the char data type and create an array
```c
char name[] = "Thomas";
printf("%s,\n", name);
printf("%c,\n", name[0])
```

- C has many String functions. To include them use the <string.h> library
Example:
```c
#include <string.h>
char string1[] = "hello";
char string2[] = " world";

char output = strcat(string1, string2)
printf("%s\n", output)
```
### user input
- user input can be stored in vars through the scanf() method
- scanf("data type specifier", &varName)
- you can also declare multiple inputs at once
  scanf("datatype1 datatype2", var name1, var name2)
- the & operator is used to pass the address of the variable where the input will be stored
```c
printf("input a number");
scanf("%d", &userNum1);

printf("input 1 chars & 1 number");
scanf("%c %d", &userChar, &userNum2);

printf("first you inputted %d \n after that you inputted: \nchar: %c \nnum: %d", userNum1, userChar, userNum2);
```
What are Format specifiers?
- Format specifiers define the type of data to be read or written. We provided each specifier in the [[C Variable types]] table.
### memory Access and pointers
```c
int var = 1;
printf("%p", &var) //this will output something like 0x7ffe5367e044
```

when using this you will get information where the var is stored in your memory (memory address)
- memory address is in hexadecimal form
- in this case &var is also referred to as a pointer
- pointer = variable which stores the memory address of another var
- pointers allow you to manipulate the data in your computers memory
**how to create a dedicated pointer var**
use the same datatype of the var which memory address you're trying to safe and add a * at the end
 ```c
 char a = "a";
 char* ptrA = &a;

printf("%p/n", &a);
printf("%p", ptrA)

//this should output the same memory addresses
```
### math functions

```c
#include <math.h>
```

- there are many math functions available using the math library
- the most commons are the following:
  1. square root- sqrt(x)
  2. rounding a number- ceil(1.4), floor(1.4)
  3. x to the power of y- pow(x,y)
- if you want to know more about the math library's capabilities click [here](https://www.w3schools.com/c/c_ref_math.php)
# Object orientated programming?
It's important to know that C is a imperativ and procedural programming language. This means that C lacks features of object orientated programming such as objects and classes which you might be familiar from e.g. Java. [[C structures]] is a new C feature which is comparable to data objects.
# Why use C in the first place
#### **Overview**
- **C is a general-purpose programming language created by Dennis Ritchie at the Bell Laboratories in 1972.**
- **C is strongly associated with UNIX, as it was developed to write the UNIX operating system.**
- **C is very fast, compared to other programming languages, like Java and Python.**  
- **A huge part is [[C Memory Management]].**
- **C is very versatile; it can be used in both applications and technologies.**

if you're interested about further information regarding:
- efficiency and performance
- flexibility and portability
- influence and legacy
- applications
- the educational value
- future of c

you can read our dedicated article [[Why Should You Use C?]]

# Optional: How does file handling work in C?
In general C's file handling is very similar to Python's implementation of file handling. If you're already familiar which that you should get the hang of it pretty easily. There are minor differences when [[handling files with C]]. Click the highlighted text when you want to know more about the topic.
# Cheatsheet
In C, you have to explicitly import libraries like `stdio.h`, `stdlib.h`, and others because C is designed to be a minimalistic language, providing only the essential tools for programming. This modular approach allows you to include only the functionality you need, keeping your program lightweight and efficient. Knowing these libraries is crucial because they provide the building blocks for tasks like input/output, memory management, and mathematical operations, which are not built into the core language itself. C's minimalism contributes to its speed, as it avoids unnecessary overhead and allows programmers to write highly optimized code. This control and simplicity make C a popular choice for system-level programming and performance-critical applications.
Click the highlighted text to see some of the most basic libraries and a few of it's function: [[C basic libraries- cheatsheet]]

# Student Challenge
To use you new knowledge about C we came up with a small [[C student challenge]]. If you want you can add a runtime output after all of the arguments are defined and we can compare them to find the fastest solution among the student group.
Here is [[sample solution(ChatGPT)]] by gpt and our [[group sample solution- student coding task]].
Happy coding and enjoy C :)


### Youtube Video
[link]([https://youtu.be/zm063gmDg_0?si=u-5LNWS6damtaTuC](https://youtu.be/zm063gmDg_0?si=u-5LNWS6damtaTuC "https://youtu.be/zm063gmDg_0?si=u-5LNWS6damtaTuC"))
We produced a 25min video where we discuss the information dealt with in this article. Note, that the video is in german and covers only the basics of this article. Topic like the structures aren't covered due to time regulation.



out sources: [[sources]]