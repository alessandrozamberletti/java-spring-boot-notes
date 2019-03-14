# Dependency Injection

* For mandatory dependencies or when aiming for immutability, use __Constructor-based Dependency Injection__
* For optional or changeable dependencies, use __Setter-based Dependency Injection__
* Avoid __Field-based Dependency Injection__ in most cases

## Constructor-based Dependency Injection

```java
@Component
public class Car {
 
    @Autowired
    public Car(Engine engine, Transmission transmission) {
        this.engine = engine;
        this.transmission = transmission;
    }
}
```

* required components are passed into a class at the time of instantiation
* Spring will initialize the instance of Car class by calling the @Autowired annotated constructor and using the predefined Engine and Transmission beans
* __NOTE__ classes with a single constructor can omit the @Autowired annotation
* __NOTE__ constructor-based injection can be leveraged in @Configuration annotated classes and if such class has only one constructor the @Autowired annotation can be omitted as well

## Setter-based Dependency Injection

```java
@Component
public class ATM {

	private Printer printer;

	public Printer getPrinter() {
		return printer;
	}

	public void setPrinter(Printer printer) {
		this.printer = printer;
	}

	public void printBalanceInformation(String accountNumber) {
		getPrinter().printBalanceInformation(accountNumber);

	}

}
```

* If Printer is a @Bean/@Component, Spring will create an instance of the Printer class and associate the instance with the "printer" member in ATM class
* however as the "printer" member in ATM class is private, the ATM class needs to expose its dependency to Spring for it to inject the Printer instance into the ATM class. e.g. If the ATM class exposes its dependency on Printer class as a setter method so that Spring can inject the Printer object then this is called as Setter injection
* Setter method injection is a very common way to resolve dependencies within the Spring framework

## Field-based Dependency Injection

```java
...
@Autowired
private Cart cart;
...
```

* Drawbacks
** You cannot create immutable objects, as you can with constructor injection
** Your classes have tight coupling with your DI container and cannot be used outside of it
** Your classes cannot be instantiated (for example in unit tests) without reflection. You need the DI container to instantiate them, which makes your tests more like integration tests
** Your real dependencies are hidden from the outside and are not reflected in your interface (either constructors or methods)
** It is really easy to have like ten dependencies. If you were using constructor injection, you would have a constructor with ten arguments, which would signal that something is fishy. But you can add injected fields using field injection indefinitely. Having too many dependencies is a red flag that the class usually does more than one thing, and that it may violate the __Single Responsibility Principle__

* You should primarily use constructor injection or some mix of constructor and setter injection
* Field injection has many drawbacks and should be avoided. The only advantage of field injection is that it is more convenient to write, which does not outweigh all the cons.

# References

* https://www.baeldung.com/constructor-injection-in-spring
* http://www.studytrails.com/frameworks/spring/spring-setter-injection/
* https://stackoverflow.com/questions/39890849/what-exactly-is-field-injection-and-how-to-avoid-it
