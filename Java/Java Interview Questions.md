# Java Interview Questions

## 1. Basic Java Questions

### 1.1 JDK, JRE, JVM

- JVM: abstract machine. It executes the bytecode and converts it to machine code.
- JRE: Java Runtime Environment. It's a runtime environment that implements JVM and provides all libraries, classes and other files that JVM uses at run time. 
- JDK: Java Development Kit. It provides the environment to **develop and execute the program**. It includes two things:
  - Development Tools (java, javac)
  - JRE

### 1.2 Synchronization?

When we have multiple threads trying to access the same resource, we implement synchronization to keep all concurrent threads in execution to be in sync.

### 1.3 Process and Thread

Process is running instance of program over the operating system, and a thread like main thread is running within the process. 

Concurrent programming: A particular task on the main thread is taking longer time to execute, the other tasks after the task will be blocked. We can bring down one more thread, offload the heavier task over the main thread to the user thread

![process and thread](process%20and%20thread.png)

### 1.4. Wrapper Class

Wrapper class converts primitives to references. You can follow OOP, you can **Pass By Reference** 

```java
public static void main(String[] args){
	int i = 10; // single value container. only contains one value
  Integer iRef = new Integer(i); // boxed (constructing the object)
  int j = iRef.intvalue(); // unboxed (extract the value from Object)
  Integer kRef = i; // AutoBoxing (Integer kRef = new Integer(i))
  int l = kRef; // AutoUnboxing
  
}
```

### 1.5. Final, Finally, Finalize

- final: It's used to apply restrictions on variables, methods and classes
  - variables can't be changed
  - methods can't be overridden
  - classes can't be inherited
- finally: It's used to place important code. It's executed whether the exceptionis handled or not. `e.g. try -> finally; catch -> finally`
- finalize: It's a destructor. It's used to perform clean up processing just before object is garbage collected.

```java
class FinalizeDemo{
	protected void finalize() throws Throwable{
		System.out.println("Obj finalized...")
	}
}
.... main(){
  FinilizeDemo fdRef = new FinalizeDemo();
  fdRef = null;
	System.gc();
}

```

### 1.6 StringBuffer and StringBuilder

Strings are immutable, while StringBuffer and StringBuilder are mutable

- StringBuffer operations are thread-safe and synchronized where StringBuilder operations are not thread-safe
- StringBuffer is to be used when multiple threads are working on the same String and StringBuilder in the single threaded environment
- StringBuilder performance is faster than String Buffer because of no overhead of synchronized

### 1.7 Stack and Heap

- Stack is the memory set aside as scratch space for a thread of execution. When a function is called, a block is reserved on the top of the stack for local variables and some bookkeeping data. Stack memory stores primitive types and the addresses of objects.
- Heap is the memory set aside for dynamic allocation. Objects. 

![](heap%20and%20stack.png)

### 1.8. ArrayList and Vector

![](ArrayList%20and%20Vector.png)

### 1.9. HashMap and HashTable

![HashMap and HashTable](HashMap%20and%20HashTable.png)

### 1.10. equals() and == operator

```java
String a = new String("a");
String b = new String("b");

a == b // => compare references, so we normally use "==" to compare primitives and objects
a.equals(b) // check the equality of two objects
```



## 2. OOP

### 2.1. Abstract classes and Interfaces

![Abstract Class and Interfaces](Abstract%20Class%20and%20Interfaces.png)

```java
abstract class Shape{
  Shape(){
    System.out.println("Shape");
  }
  abstract void draw();
}

class Circle extends Shape{
  void draw(){
    //overriding
    System.out.println("Circle");
  }
}

class Rectangle extends Shape{
  void draw(){
    System.out.println("Rectangle");
  }
}

public static void main(String[] args){
  Shape s;
  s = new Circle();
  s.draw(); // draw a circle
  
  s = new Rectangle();
  s.draw(); // draw a rectangle
}
```

```java
interface Shape{
  void draw();
}

class Circle implements Shape{
  void draw(){
    //overriding
    System.out.println("Circle");
  }
}

class Rectangle implements Shape{
  void draw(){
    System.out.println("Rectangle");
  }
}

public static void main(String[] args){
  Shape s;
  s = new Circle();
  s.draw(); // draw a circle
  
  s = new Rectangle();
  s.draw(); // draw a rectangle
}
```

Abstract class is like the parent, while interface is like the rule. You inherit from the parent, and you need to follow the rules.

### 2.2 Run-time Polymorphism

Polymorphism: It's a characteristic of being able to assign a different meaning or usage to something in different contexts.

Run-time polymorphism: It's a process in which a call to an overridden method is resolved at runtime rather than at compile-time.

In this process, an overridden method is called through the reference variable of a superclass. 

### 2.3 Method Overriding and Method Overloading

![](method%20overriding%20and%20method%20overloading.png)

### 2.4. Can you override a private or static method?

- Private methods cannot be overridden because they are not visible from any other class.
- For static method: If you create a similar method with same return type and same method arguments in child class then it will hide the super class method. This is known as method hiding. It's DIFFERENT from method overriding. BTW, Static methods should be called on CLASS.

### 2.5. Multiple inheritance

Multiple inheritance: one class extends from multiple classes. It is NOT SUPPORTED in Java.

## 3. Servlets

### 3.1. What is Servlet?

- Java Servlet is server side technologies to extend the capability of web server by providing support for dynamic response and data persistence.
- The javax.servlet and javax.servlet.http packages provide interfaces and classes for writing our own servlets.
- All servlets must implement the javax.servlet.Servlet interface, which defines servlet lifecycle methods
- As most web applications are accessed using HTTP protocal, we mostly extrend HttpServlet class

### 3.2. Get and Post method

![get and post](get%20and%20post.png)

### 3.3. Session Management in servlets?

- Session is a conversational state between client and server and it can consists of multiple request and response between client and server

- Since HTTP and Web Server both are stateless, the only way to maintain a session is when some unique information aobut the session(session id) is passed between server and client in everyrequest and response.

  ![session management](session%20management.png)

### 3.4. ServletContext and ServletConfig

![serveletContext vs serveletConfig](serveletContext%20vs%20serveletConfig.png)

### 3.5. Life-cycle of servlet

loading -> instatiating -> initializing -> request -> destruction

3 API: init, service, destroy

### 3.6. Request Dispatcher

RequestDispatcher interface is used to forward the request to another resource that can be HTML, JSP or another servlet in the same application

We can also use this to include the content of another resource to the response.![RequestDispatcher](RequestDispatcher.png)

### 3.7. Cookies

Cookies are text data sent by the server to the client and they are saved at the client's local machine.

- Servlet Cookie API: javax.servlet.http.Cookie `e.g. getCookies(); addCookie(Cookie c)` 

## 4. JDBC 

