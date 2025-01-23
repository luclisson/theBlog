create a new java class called xController
### get request
- add @RestController above the class
- inside the class define a public method which returns something (usually a string)
- add @RequestMapping(method = RequestMethod.GET, path = "/test") annotation
alternatively you can use
- add @GetMapping(path = "/test")
### post request
- write a method like get method
```java
@PostMapping(path="/this/is/a/path")
public void createUser(@RequestBody User exampleUser){
	daoService.saveUser(exampleUser);
}
```
- in the request you have to pass a body with the structure of the User object (at least in this example)
- when you received the body you can use the [[dao service]] to pass the new value to your datahub like a database or something else (use dao service to add readability and structure to your code)
- the browser can't send post request by itself. To test your post request you can use the [talend api tester](https://chromewebstore.google.com/detail/talend-api-tester-free-ed/aejoelaoggembcahagimdiliamlcdmfm) and send a post request with a body. Alternatively you could send post request with code using e.g. js
- for later debugging you should return the response status with a return statement like this
  ```java
  return ResponseEintity.created(null).build()
```
	with the help of ResponseEntity you can return your needed response like success, error or created. In the parameter you could add the location. I can't really explain the build() method

	the uri location is the path
	how to get current request uri
```java
URI location = ServletUriComponentsBuilder.fromCurrentRequest();
//to add path var or something else
URI location = ServletUriComponentsBuilder.fromCurrentRequest()
				.path("/{id}").buildAndExpand(exampleUser.getId).toUri;


//then you can return the location instead of null
return ResponseEintity.created(location).build()
```

	NOTE!
	you need to use the returned obj in the definition of the function
```java
@PostMapping(path="/this/is/a/path")
public ResponseEntity<user> createUser(@RequestBody User exampleUser){
	daoService.saveUser(exampleUser);
return ResponseEntity.created(null).build();
}
```


### different response status
- resource is not found: 404
- server exception, server error: 500
- validation error: 400
- success: 200
- a resource is created: 201
- no content: 204
- unauthorized: 401