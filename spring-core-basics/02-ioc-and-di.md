# IoC

- IoC stands for **Inversion of Control** .
- It means , instead of you creating the objects Spring creates and manages them for you.
- Usually you control object creation, this is called **tight coupling**.
- Inversion of Control means giving the control of object creation to the framework,instead of you doing it yourself.


### Why it is called Inversion of Control?

| Without Spring                        | With Spring (IoC)               |
| ------------------------------------- | ------------------------------- |
| Developer controls object creation    | Spring controls object creation |
| You decide how/when to create objects | Spring decides                  |
| Your code is tightly coupled          | Your code is loosely coupled    |

<img width="1283" height="516" alt="image" src="https://github.com/user-attachments/assets/b517257e-8ae2-4842-8f58-ba24cd4ab5eb" />


## DI

- DI stands for Dependency Injection.
- When one class needs another class, Spring injects that dependency automatically.
- A “dependency” means something your class needs.

#### Example

- Without DI

```java
// Engine class
class Engine {
    void start() {
        System.out.println("Engine started");
    }
}

// Car class
class Car {
    private Engine engine;
    
    public Car() {
        this.engine = new Engine();
    }
    
    public void drive() {
        engine.start();
        System.out.println("Car is running...");
    }
}

public class MainWithoutDI {
    public static void main(String[] args) {
        Car car = new Car();
        car.drive();
    }
}
```

- Using DI


1. Creates Engine class

```java
import org.springframework.stereotype.Component;

@Component
public class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}
```

2. Injects it(dependency) into Car class

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class Car {

    private final Engine engine;

    @Autowired
    public Car(Engine engine) {  // ✔ Dependency Injection
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is running...");
    }
}
```

3. Main

```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.beans.factory.annotation.Autowired;

@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private Car car;   // Spring injects Car (and also Engine inside Car)

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        car.drive();
    }
}
```

## Tyoes of Injectsion

1. Constructor Injection
2. Field Injection
3. Setter Injection

### Constructor Injection
