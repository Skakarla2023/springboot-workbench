## @GetMapping

- @GetMapping is used when you want to get/fetch/read data from the server.
- When someone sends a GET request to your API URL, this method will run.

```java
@RestController
public class DemoController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello from GET!";
    }
}
```

- 📌 GET requests do not send body data.
- They are mainly used to fetch things.





## @PostMapping

- @PostMapping is used when you want to send/create/add data to the server.
- A POST request sends data (usually JSON) from client → server.

```java
@RestController
public class UserController {

    @PostMapping("/add-user")
    public String addUser(@RequestBody User user) {
        return "User saved: " + user.name;
    }
}

class User {
    public String name;
    public int age;
}
```

#### 📌 Client sends JSON:

```json
{
  "name": "Satwika",
  "age": 21
}
```

#### The API returns:

```sql
User saved: Satwika
````
