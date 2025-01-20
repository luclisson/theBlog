- you need to install a C compiler inorder for your computer to understand the language
```c
#include <stdio.h>  
  
int main() {  
  printf("Hello World!");  
  return 0;  
}

```

- stdio.h is the header library which is used to handle in and output (you will see this line in nearly every project)
- any code that is inside the main function will be executed when you build and run the program
- the "int" infront of main() is used to define what var type the function returns. In this case its an int (0). Alternatively you could use void if you dont want to return anything it would look like this:
  ```c
  #include <stdio.h>  
  
	void main() {  
	  printf("Hello World!");    
	}
	```

### Compiler

To run you C programs outside of your IDE e.g. visual studio code, you have to install a c compiler. Here, we will provide you with some instructions and resources how to install a compiler and how to use a compiler.

#### **How to install a compiler**
Since there isn't a official c compiler published by c, we have to download a third party compiler. 

Windows: 
- you can install [MinGW](https://sourceforge.net/projects/mingw/) and select the c compiler in the installation process
- you have to add your c compiler installation path to your environment variables in order to use it in powershell
we found a great youtube video which shows excactly how to install a c compiler on windows.

MacOS/Unix:
- we recommend to install gcc via a package manager
  for mac you could use [homebrew](https://brew.sh/) 
  your favourite package manager should work perfectly fine as well
```shell
brew install ghc
```
- the command "ghci" should work (if not check your ~/.zshrc file and add ghci as export path)

#### How to compile a c file
**windows**
1. check your compiler
```shell
gcc --version
```
2. open the files location in the terminal
3. compile the c file
```shell
gcc myFile.c
```
--> this will create a .exe file
4. run the .exe file
macOS/Unix
1. check your compiler
```shell
gcc --version
```
2. open the file's location in the terminal
3. compile the c file
```shell
gcc myFile.c -o myFile
```
4. run the compiled file
```shell
./myFile
```
