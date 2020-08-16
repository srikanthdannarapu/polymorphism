# polymorphism
The ability of an object to behave differently in different situations is called Polymorphism. This concept is core to object oriented programmer and key to programming in Java. There are two types of polymorphism prevalent in Java; Static Polymorphism and Dynamic Polymorphism. As a Java developer, you will routinely use each type of polymorphism.

### Types of Polymorphism
#### Static Polymorphism
In a Java program, it is possible to have two or more methods in the same class having the same name but with different argument lists. The argument lists can differ in the number of parameters, data type of parameters and the sequence of data type of parameters. This is called static polymorphism. It is also commonly known as method overloading. The correct method to be called is selected on the basis of the argument list. Note that the return type of the method has no bearing on it’s behavior in terms of static polymorphism.

The class below is an example of Static Polymorphism.
```java
public class StaticPolymorphism {
    void test (int a) {
        System.out.println("Method A - The value of a is: "+ a);
    }

    void test (int a, int b) {
        System.out.println("Method B - The values of a and b are: "+ a +", "+ b);
    }

    double test (double a) {
        System.out.println("Method C - The value of a is: "+ a);
        return a*a;
    }
}
```

In this example, three methods with the name of test have been defined. Each differs in its argument lists. In the first method, only one parameter is present having data type int. In the second method, two parameters are present, both with data types int. And in the third method, there is only one parameter with data type double. The name of all the three methods is same, but their argument lists are different. This is what makes them overloaded methods.

#### Static Polymorphism in Action
We can write a unit test for our example class to observe Static Polymorphism at work. In our test, each method is called with the proper argument list.
```java
public class StaticPolymorphismTest {

    @Test
    public void testPlymorphism(){
        StaticPolymorphism staticPolymorphism = new StaticPolymorphism();

        staticPolymorphism.test(12);
        staticPolymorphism.test(2, 3);

        double testValue = 1500;
        double result  = staticPolymorphism.test(testValue);
        System.out.println("Test Result is: " + result);
    }
}
```
If we run our test, we can observe the following results:
```text
Method A - The value of a is: 12
Method B - The values of a and b are: 2,3
Method C - The value of a is: 1500.0
Test Result is: 2250000.0
```
Just like methods, constructors can also be overloaded. We generally have two types of constructors, default constructor and parametrized constructor. Which among the default constructor or the parametrized constructor will get invoked, depends on the type of constructor which is invoked during the object creation. We can use the this() invocation to invoke one constructor from another one. We just need to pass the proper parameters for invoking the appropriate constructor using the this() invocation.

Static Polymorphism is often used when you have a list of parameters for a method or constructor call and you wish to default some of the values. You can use Static Polymorphism to provide alternate implementations of methods or constructors which supply default values for the optional parameters.

#### Dynamic Polymorphism
Dynamic polymorphism is a key concept in Object Oriented programming. If you wish to become an effective Java programmer, you will need to have a firm understanding of Dynamic Polymorphism. Consider the following class:
```java
public class Vehicle {

    protected String manufacturer = "Unknown";

    public void vehicleName() {
        System.out.println("I'm a vehicle.");
    }
}
```
We implement dynamic polymorphism in Java by extending classes. Consider this example:

```java
public class Car extends Vehicle {
    private Integer numberOfWheels = 4;
    
    @Override
    public void vehicleName() {
        System.out.println("I am a car.");
    }
}
```
Here we have a Car  object which extends our Vehicle  class. We are free to add properties to our extended class as we have done with the numberOfWheels  property.

In this example, we are also overriding the vehcileName  method of the base class. While you are not required to, in this example, we are using the @Override  annotation on the vehicleName  method. This tells the Java compiler you wish to override the method of the base class. If the signature of the method does not match a signature of a method on the base class a compiler error will be thrown. This helps prevent you from accidentally introducing a new method, rather than overriding the method of the base class. It also aids in the readability of your source code for other programmers. Your intention of overriding a method of the base class is clear. While you are not required to use the @Override  annotation, it is considered a best practice to use.

Through polymorphism, your base class can be extended to handle other use cases.
```java
public class Motorcycle extends Vehicle {

    private Integer numberOfWheels = 2;

    @Override
    public void vehicleName() {
        System.out.println("I am a motorcycle.");
    }
}
```
In the example above, we’ve extended our base Vehicle class with a Motorcycle class. Following the concepts of Object Oriented Programming, using polymorphism, we could have additional classes things such as Boat, Plane, Bicycle, Truck, Armored Tank. While each of our use cases are different, each is technically a vehicle. This gets us to the classic Object Oriented programming “Is a” test.

* A Car  is a Vehicle .
* A Motorcycle  is a Vehicle .
* A Boat  is a Vehicle .
* A Armored Tank  is a Vehicle .
You are not limited to extending a class just once. Consider this example:

```java
public class Corvette extends Car{

    protected String manufacturer = "General Motors";
    private Integer numberOfWheels;
    private Boolean hasSupercharger;

    @Override
    public void vehicleName() {
        System.out.println("Zoom, zoom, I'm a Corvette.");
    }

    public void goFast(){
        System.out.println("Zoom.....");
    }
}
```
Here we have a Corvette class which extends our Car class, which extends our Vehicle class.

* A Corvette  is a Car .

* A Car  is a Vehicle .

It is common when using polymorphism in object oriented programming for your extended classes to become more and more specialized. In our Corvette  example, you can see how our new class has additional properties and methods specific to the Corvette  object. Consider how your class would change if it was a Plane  or a Boat  object.

#### Dynamic Polymorphism In Action
A child class object can be assigned to a parent class reference. The syntax for the same has been given below,

Vehicle vehicle = new Corvette();

We can write a unit test using JUnit to demonstrate this with our examples so far.

```java
@Test
public void testDynamicPolymorphism(){
    List<Vehicle> vehicles = new ArrayList<>();
    vehicles.add(new Vehicle());
    vehicles.add(new Car());
    vehicles.add(new Motorcycle());
    vehicles.add(new Corvette());

    for(Vehicle vehicle : vehicles){
        vehicle.vehicleName();
    }
}
```