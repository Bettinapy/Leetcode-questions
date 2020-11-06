# Java for programmers

### Module 1: Basics of Java Programming

#### 1. Print

##### 1.1. print to the screen

`System.out` is also the name of an object: the main printed output device for your program. So `System.out.println` calls the method `println` on the `System.out` object.

**note:** The `System.out.println` method prints a newline after the text. Use `System.out.print` if you don’t want the newline.

##### 1.2. Format

```java
class printExamples {
  public static void main(String args[]) {
    System.out.format("My favorite number is %.3f.\n", 3.141592654); 
    
    // part of a times table:
    System.out.format("%2d %2d %2d\n", 4, 6, 8);
    System.out.format("%2d %2d %2d\n", 8, 12, 16);
  }
}
```

Output

My favorite number is 3.142. 

4   6   8 

8 12 16



#### 2. Variables

**Java is a `statically-typed` language, which means that you must `explicitly create each variable and tell what type of data (for example, an integer) that variable will store before using it`.

##### 2.1. Naming convention

Camel case

##### 2.2. Variable declaration

int thisIsMyInt => after you declare it, you cannot change the type, if the type is not matched, a wrong message will be returned at compile time



#### 3. Method parameters

##### 3.1. Method overloading and method signature

In Java, you can write two different methods with the same name in the same class, as long as the methods take different parameter types. 

The name of a method, together with the types of its parameters in order, is called the **method signature**.



```java
class Overload {
  
  public static void printMyFavoriteNumber(int x) {
    System.out.println("My favorite number is the integer " + x);
  }
  
  public static void printMyFavoriteNumber(double x) {
    System.out.println("My favorite number is the double " + x);
  }
  
  public static void main(String[] args) {
    printMyFavoriteNumber(42);
    printMyFavoriteNumber(3.1415);
  }
  
}
```

##### 3.2. Method return values

you must declare the type of return values when you declare the class, otherwise, the compiler will indicate an invalid return type.

```java
public static double square(double x) {
    return x * x;
  }
```

Every method must have its return type declared, even if the method has no return value. A function for drawing a smile, for example, might not return anything at all, so it should have a return type of `void`

##### 3.3. Main method

The method `main` is declared with `public static void`. The `void` indicates that `main` does not return a value. 

##### 3.4. Exiting a program

Java can exit prematurely and indicate success or failure to the operating system using `System.exit()`. Even if you don’t care about the resulting value, `System.exit()` is occasionally useful for debugging, or for terminating a program early for other reasons.

#### 4. String and Class

**A class in Java has two purposes:**

1. A class is a collection of methods that you may call.
2. A class defines a custom data type, and can be used to make objects of that class.

##### 4.1. Static and non-static method in String

Static methods do not need access to a particular string object’s data. The static `valueOf` method takes a parameter that is not a String, and creates a String. 

Non-static methods require a string as input, and instead of passing that string as a parameter, dot-notation is used: `s.toUpperCase()`. It’s possible that there might be other methods named `toUpperCase` out there. Java knows which method to call because Java knows that `s` is a String, so Java looks in `String.java` for the method.

static: called on Class

non-static: called on an object 

##### 4.2. Primitive data type

Data types like `int`, `double`, and `boolean` in Java are called *primitive data types*, because variables of those types are built-in, and `do not have methods available to act on them.` `char` is also a primitive data type, representing a single character of text.

To distinguish between `String` and `char` data, Java uses single quotes for character literals and double quotes for Strings

##### 4.3. Strings are immutable in Java

e.g. String.toUpperCase does not change the string. it creates a new string that is uppercased and returns the new string



#### 5. Arrays

##### 5.1. Arrays cannot be resized

##### 5.2. Initialize array with `new`

```java
int[] newArray;
newArray = new int[7];
```

##### 5.3. Array in main (String[] args)

In Java `args` contains the supplied [command-line arguments](http://docs.oracle.com/javase/tutorial/essential/environment/cmdLineArgs.html) as an array of `String` objects.

In other words, if you run your program as `java MyProgram one two` then `args` will contain `["one", "two"]`.

If you wanted to output the contents of `args`, you can just loop through them like this...

```java
public class ArgumentExample {
    public static void main(String[] args) {
        for(int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```

https://stackoverflow.com/questions/890966/what-is-string-args-parameter-in-main-method-java

##### 5.4. `java.util.Arrays` class

import java.util.Arrays;

#### 6. foreach-loops

```java
class ForEachExample {
  public static void main(String[] args) {
    int[] primes = {2, 3, 5, 7, 11, 13};
    for(int p: primes) {
      System.out.println(p);
    }
  }
}

```



### Module 2: Object Oriented Programming

#### 1. Classes and Objects

##### 1.1 Intro

**Classes** are the building blocks of programs built using the object-oriented methodology. Such programs consist of *independent self-managing modules and their interactions.*

The concept of classes allows us to create complex objects and applications in Java. This is why classes are the basic building blocks behind all of the OOP’s principles.

An **object** is an instance of a module, and a class is its definition.

##### 1.2 Access Modifiers

```java
Access Levels
Modifier        Class    Package    Subclass    World
-----------------------------------------------------
public           Y        Y          Y           Y
protected        Y        Y          Y           N
(Default)        Y        Y          N           N
private          Y        N          N           N
```

##### 1.3 Fields

- Static: resides in a class. All the objects we create will share this field and its value. `e.g. static int number`
- Non-static: resides in the instances of a class. `e.g. int number`
- Final: cannot have its value changed once it is assigned. `e.g. final int number = 4`

##### 1.4 Methods

Advantages of method overloading: 

- save method name, save memory
- increase execution speed
- make code cleaner and readable
- allow the implementation of polymorphism

##### 1.5 Constructor

The constructor is used to *construct* the object of a class. A constructor’s **name** must be exactly the **same** as the name of its class.

```java
class Date {

  private int day;
  private int month;
  private int year;
  private String event;


  // Default constructor
  public Date() {
    // We must define the default values for day, month, and year
    this.day = 0;
    this.month = 0;
    this.year = 0;
  }

  // Parameterized constructor
  public Date(int day, int month, int year){
    // The arguments are used as values
    this.day = day;
    this.month = month;
    this.year = year;
  }
  
  // Parameterized constructor
  public Date(int day, int month, int year, String event){
    this(day, month, year); // calling the constructor
    this.event = event;
  }

  // A simple print function
  public void printDate(){ 
    System.out.println("Date: " + day + "/" + month + "/" + year + "  --> " + event);
  }
  
}

class Demo {
  
  public static void main(String args[]) {
    // Call the Date constructor to create its object;
    Date date = new Date(1, 1, 2019, "New Year"); // Object created with specified values! // Object created with default values!
    date.printDate();
  }
  
}
```

#### 2. Data hiding

##### 2.1 Encapsulation

Encapsulation is a fundamental programming technique in OOP used to achieve data hiding.

**Encapsulation** in OOP refers to binding the **data** and the **methods to manipulate that data** together in a single **unit** (class).

My understanding: declare the variables `private` and the methods which provide an interface to access those fields are public.



#### 3. Inheritance

- **SuperClass (Mother Class or Base Class):** This class allows the *re-use* of its `non-private` members in another class.
- **SubClass (Child Class or Derived Class):** This class is the one that *inherits* from the superclass.

##### 3.1. Super 

the `super` keyword in Java is used to refer to the *SuperClass* members from inside the immediate *Subclass*.

Use cases:

- access parent class fields: `super.fuelCap`
- call a parent class method: `super.display()`
- using with constructors: `super(parameters)`

##### 3.2. Advantages of using inheritance

- Re-usability: avoid redundant coding and save time and effort
- Avoid duplication of code
- Extensibility
- Data hiding: The base class can decide to keep some data private so that it cannot be altered by the derived class.

#### 4. Polymorphism

##### 4.1. Intro

Different subclasses inherit from the same superclass. In all of the subclasses, all methods inherited from the superclass can be reimplemented in their own way. 

##### 4.2. Method overriding

Advantages:

- The derived classes can give their own specific implementations to inherited methods without modifying the parent class methods.
- For any method, a child class can use the implementation in the parent class or make its own implementation.

##### 4.3. Method overloading and overriding

| **Method Overloading**                                       | **Method Overriding**                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Overloading happens at **compile time.**                     | Overriding happens at **runtime**                            |
| Gives better performance because the binding is being done at compile time. | Gives less performance because the binding is being done at run time. |
| **Private** and **final** methods can be overloaded.         | **Private** and **final** methods can not be overridden.     |
| Return type of method does not matter in case of method overloading. | Return type of method must be the same in the case of overriding. |
| Arguments must be different in the case of overloading.      | Arguments must be the same in the case of overriding.        |
| It is being done in the same class.                          | Base and derived classes are required here.                  |
| Mostly used to increase the readability of the code.         | Mostly used to provide the implementation of the method that is already provided by its base class. |

##### 4.4 Dynamic polymorphism

**Dynamic polymorphism** is the mechanism by which methods can be defined with the same name, return type, and parameters in the base class and derived classes.

This is decided during runtime and is, therefore, called **dynamic** or **runtime** polymorphism.

##### 4.5. Static and Dynamic Polymorphism

- **Static polymorphism** is also known as compile time polymorphism.
- **Dynamic polymorphism** is also known as runtime polymorphism.

| **Static Polymorphism**                                      | **Dynamic Polymorphism**                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Polymorphism that is resolved during compile time is known as static polymorphism. | Polymorphism that is resolved during run time is known as dynamic polymorphism. |
| Method overloading is used in static polymorphism.           | Method overriding is used in dynamic polymorphism.           |

#### 5. Abstract Classes and Interfaces

**Abstraction** in Object-Oriented Programming refers to showing only the essential features of an object to the user and hiding the inner details to reduce complexity. 

What ? (yes) How? (no)

##### 5.1. Abstract classes and methods

A method with the keyword `abstract` in its declaration is known as an **abstract method**.

###### 5.1.1 Abstract Methods

Rules: 

- In contrast to a concrete/normal Java method an **abstract method** does not have a body/definition i.e. it only has a declaration or method signature inside an *abstract class or an interface* (more on these later).
- An **abstract method** can be declared inside an *abstract class* or an *interface* only.
- In other words, it can be said that to contain any **abstract method** in its implementation a class has to be declared as an *abstract class* because *non-abstract classes* **cannot** have abstract methods.
- An *abstract method* **cannot** be declared *private* as it has to be implemented in some other class.

###### 5.1.2 Abstract Classes

Rules:

- An abstract class ***cannot*** be instantiated i.e. one cannot create an object of an *abstract class*.
- An *abstract class* can have the declaration of *abstract method(s)* (as an abstract method’s body cannot be implemented in an abstract class) but it is not compulsory to have any.
- Non-abstract/normal methods can be implemented in an **abstract class**.
- To use an *abstract class* it needs to be **inherited from**.
- The class which *inherits* from the *abstract class* **must** implement all the *abstract methods* declared in the *parent abstract class*.
- An abstract class can have everything else as same as a normal Java class has i.e. constructor, `static` variables and methods.

##### 5.2 Interfaces

An interface is just like a `class` and specifies the behavior that a class **must** *implement*.

Rules:

- An interface can have:
  - `abstract` method(s)
  - `default` method(s)
  - `static` method(s)
  - `public static final` variable(s)
- All the methods declared or implemented in an interface are by default `public` and all the variables are by default `public static final`.
- Just like an `abstract` class, an `interface` cannot be instantiated.
- To use an interface, a class **must** `implement` all of the `abstract` method(s) declared in it.
- An interface **cannot** have constructor(s) in it.
- A class cannot extend from more than one class, but it can implement **any number** of interfaces.”?
- An interface can `extend` from another interface.
- An interface cannot be declared `private` or `protected`.

Advantages:

- Interfaces allow us to achieve *100% abstraction*.
- Interfaces can be used to achieve *loose coupling* in an application. This means that a change in one class doesn’t affect the implementation of the other class.
- By the use of interfaces, one can break up complex designs and clear the dependencies between objects.
- Interfaces can be used to achieve *multiple inheritance*

##### 5.3 Default methods and static methods

The static methods in interfaces are similar to default methods but the only difference is that you can’t override them.

##### 5.4 Functional Interface

Any interface that has only one abstract method can be annotated with the `@FunctionalInterface` annotation.

##### 5.5 Interface vs Abstract class

| **Interfaces**                            | **Abstract Classes**                                  |
| ----------------------------------------- | ----------------------------------------------------- |
| Can have abstract method(s) only.         | Can have concrete (non-abstract) & abstract method(s) |
| Support multiple inheritance              | Don’t support multiple inheritance                    |
| All members are `public`                  | Can have `private`, `protected` and `public` members  |
| All data members are `static` and `final` | Can have non-static and non-final members too         |
| Can’t have constructors                   | Constructors can be defined                           |

#### 6. Aggregaion and Composition

- Is A
- Part of: one class object is a **component** of another class. `e.g. Composition`
- Has A: one class contains a reference to another class' object `e.g. Aggregation`

##### 6.1 Aggregation

In **aggregation**, the lifetime of the owned object does not depend on the lifetime of the owner.

My understanding: A person object has a reference to a country object. The person object can be deleted, but the Country object is still there

##### 6.2 Composition

In **composition**, the lifetime of the owned object depends on the lifetime of the owner.

My understanding: A car is composed of engine, tire, door. If a delete the car object, engine, tire and door will be deleted as well.



### Module 3 Lambdas and Stream APIs

#### 1. Taste of lambdas

A **lambda expression** is just an anonymous function, i.e., a function with no name and that is not bound to an identifier. We can pass it to other methods as parameters, therefore, using the power of functional programming in Java.

```java
@FunctionalInterface
public interface Greeting {
    void greet();
}

public class WellWisher {

    public static void wish(Greeting greeting) {
        greeting.greet();
    }

    // Passing a lambda expression to wish method.
    public static void main(String args[]) {
        wish( () -> System.out.println("Namaste") );
    }
}
```

##### 1.1 Java Comparator Using Lambda

```java
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class PersonService {

    public static List<Person> getPersons(List<Person> persons) {
        // Instead of creating an anonymous class, we have provided a lambda expression.
        Collections.sort(persons, (p1, p2) -> p1.getName().compareTo(p2.getName()));
        return persons;
    }
}
```

