
syntax for the path in the GetMapping
```java

@GetMapping(path = "/this/is/a/path/{value}") //url /this/is/a/path/testValue
public String getParameter(@PathVariable String value){
	return value;
}
//this would return testValue
```

using a path variable lets you receive data through the path