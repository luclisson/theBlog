
- you can imagine structures as some sort comparable to basic data objects as in objects orientated programming but there are some major differences as well which are the following:
	1. c structures can **only contain data members (variables)** and not methods as in e.g. java. Therefore you can't define a constructors, destructors or other methods
	2. **c structures do not support encapsulation**.
	   all the so called members are public by default and there isn't a build in way to change them to e.g. private or restrict their access in general.
	3. c structures **do not support inheritance or polymorphism** (can't derive parent structure)
	4. you have to manually free memory if you don't need it anymore. There is no 'Garbage Collector' like in Java so the developer doesn't have to worry about memory.
	5. you can't assign strings to the var like you learned above, but there is a function called strcpy()
```c
//defining customer structure's members
struct customer{
	char fullName [50];
	int age;
	char mailAddress [100];
}
int main(){
	//creating a struct var
	struct customer firstCustomer;
	//accessing members of customer structure via '.'
	strcpy(fistCustomer.fullName, "Max Mustermann");
	firstCustomer.age = 25;
	strcpy(fistCustomer.mailAddress, mustermann.max@googlemail.com);
	//different syntax
	struct testStructure{
		int num;
		char letter;
		char word [30];
	}
	struct testStructure test = {1, "a", "some text"}
	//using this syntax you don't have to use the strcpy() method

	return 0;
}
```
