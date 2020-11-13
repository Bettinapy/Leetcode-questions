# Java Syntax

### 1. Java compiler

**Program in Java** -------- Java compiler -------> **Bytecode** ---------- JVM ----------> **Machine code**

This allows programs written in Java to be run on virtually any device: computers, smartphones, ATMs, toasters and even credit cards!

### 2. Primitive data type

Variables are divided into two types:

- Primitive types: store value directly. `e.g. int, char, boolean,,`
- Reference types: store a reference to an object. everything else than primitive. We use classes to create them.

When a primitive variable is assigned, the value is **copied**. If a reference is assigned, only the address of the object is copied. The object itself **isn't copied**.

### 3. Visibility of variables

|             Modifiers             | Access from… |             |           |
| :-------------------------------: | :----------: | :---------: | --------- |
|                                   |  Own class   | Own package | Any class |
|            **private**            |     Yes      |     No      | No        |
| No modifier (**package-private**) |     Yes      |     Yes     | No        |
|            **public**             |     Yes      |     Yes     | Yes       |

### 4. Concatenation

If we 'add' (+) a string and something else, then the 'something else' is implicitly converted to a string via the toString() method.

| Code                                                      | Equivalent code                                              |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| `Cat cat = new Cat(); String text = "The cat is " + cat;` | `Cat cat = new Cat();` `String s = cat.toString();` `String text = "The cat is " + s;` |

#### 4.1 Escaping characters

```java
 String windows = "This is a Windows path: \"C:\\Program Files\\Java\\jdk1.8.0_172\\bin\"";
 String javaString = "This is a Javastring:\\\"C:\\\\ProgramFiles\\\\Java\\\\jdk1.8.0_172\\\\bin\\\"";
        System.out.println(windows);
        System.out.println(javaString);
```

This is a Windows path: "C:\Program Files\Java\jdk1.8.0_172\bin" 

This is a Java string: \"C:\\Program Files\\Java\\jdk1.8.0_172\\bin\"

#### 4.2. Concatenate ArrayList when ArrayList is not a String list

```java
package com.codegym.task.task09.task0923;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;
import java.util.stream.Collectors;

/* 
Vowels and consonants

*/

public class Solution {
    public static char[] vowels = new char[]{'a', 'e', 'i', 'o', 'u'};

    public static void main(String[] args) throws Exception {
        // write your code here
        ArrayList<Character> wordVowels = new ArrayList<Character>();
        ArrayList<Character> wordConsonants = new ArrayList<Character>();
        
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        String s = reader.readLine();
        String[] words = s.split(" ");
        
        for(int i = 0; i < words.length; i++){
            for(int j = 0; j < words[i].length(); j++){
                Character wordChar = words[i].charAt(j);
                if(isVowel(wordChar)) wordVowels.add(wordChar);
                else wordConsonants.add(wordChar);
            }
        }
        String lineVowels = wordVowels.stream().map(Object::toString)
                            .collect(Collectors.joining(" "));
        String lineConsonants = wordConsonants.stream().map(Object::toString)
                                .collect(Collectors.joining(" "));
        
        System.out.println(lineVowels + " ");
        System.out.println(lineConsonants + " ");
    }

    // The method checks whether a letter is a vowel
    public static boolean isVowel(char c) {
        c = Character.toLowerCase(c);  // Convert to lowercase

        for (char d : vowels)   // Look for vowels in the array
        {
            if (c == d)
                return true;
        }
        return false;
    }
}
```



### 5. Keyboard Input

```java
package com.codegym.task.task03.task0319;

/* 
Predictions

*/

import java.io.*;

public class Solution {
    public static void main(String[] args) throws Exception {
        //write your code here
        InputStream inputStream = System.in;
        InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
        BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
        
        String name = bufferedReader.readLine();
        String number1 = bufferedReader.readLine();
        String number2 = bufferedReader.readLine();
        
        System.out.println(name + " will receive " + number1 + " in " + number2 + " years.");
    }
}

```

### 6. Static vs. Non-static

#### 6.1. Static & non- static variables/methods 

- static variables/methods are called on Class
- non-static variables/methods are called on the instance of the class

** Static methods can't address non-static methods or non-static variables! When you call a static method, you are actually passing null as the argument, so the static methods don't have access to the object and its non-static variables.

#### 6.2. Static & non-static classes

Special: difference between static and non-static nested classes:

1. A static nested class may be instantiated without instantiating its outer class. `e.g. OuterClass.StaticClass staticClass = new OuterClass.StaticClass() `
2. Inner classes can access both static and non-static members of the outer class. A static class can access only the static members of the outer class.

** The main purpose of using the **static** modifier in the class declaration is to control the relationship between the **Cat** and **StaticClassExample** classes. The idea is roughly this: the Cat class is not linked to StaticClassExample objects and can't access the instance (non-static) variables of the StaticClassExample class.

```java
package com.codegym.task.task06.task0614;

import java.util.ArrayList;

/* 
Static cats

*/

public class Cat {
    //write your code here
    public static ArrayList<Cat> cats = new ArrayList<Cat>();

    public Cat() {
        //System.out.println(Cat.cats);
    }

    public static void main(String[] args) {
        //write your code here
        for(int i = 1; i<= 10; i++){
            Cat cat = new Cat();
            cats.add(cat);
        }
        printCats();
    }

    public static void printCats() {
        //write your code here
        for(int counter = 0; counter < Cat.cats.size(); counter++){
            System.out.println(Cat.cats.get(counter));
        }
    }
}

```

##### 6.2.1 Minimum number of statics (hard) -- understand static 

```java
package com.codegym.task.task06.task0616;

/* 
Minimum number of statics

*/

public class Solution {
    // we need to make step STATIC because on line 21, we create a new Solution instance,
    // then we call method3, then method4, if step is not static, every time step will be reset to task0616
    // and step will never be greater than 1, causing the infinite loop
    // if we make step static, we can increment step every time we create a new Solution instance
    
    public static int step;

    public static void main(String[] args) {
        method1();
    }

    public static void method1() {
        method2();
    }

    public static void method2() {
        new Solution().method3();
    }

    public void method3() {
        method4();
    }

    public void method4() {
        step++;
        for (StackTraceElement element : Thread.currentThread().getStackTrace())
            System.out.println(element);
        if (step > 1)
            return;
        main(null);
    }
}

```



### 7. Comparison

| Code | Explanation                                                  |                                                              |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | `int a = 5; int b = 5; System.out.println(a == b);`          | Compare primitive types. **true** will be displayed on the screen. |
| 2    | `Cat cat1 = new Cat("Oscar"); Cat cat2 = cat1; System.out.println(cat1 == cat2);` | Compare references. **true** will be displayed on the screen. Both variables store references to the same object. |
| 3    | `String s = new String("Mom"); String s2 = s; System.out.println(s == s2);` | Compare references. **true** will be displayed on the screen. Both variables store references to the same object. |
| 4    | `Cat cat1 = new Cat("Oscar"); Cat cat2 = new Cat("Oscar"); System.out.println(cat1 == cat2);` | Compare references. **false** will be displayed on the screen. The two variables reference identical Cat objects, but not the same one. |
| 5    | `String s = new String("Mom"); String s2 = new String("Mom"); System.out.println(s == s2);` | Compare references. **false** will be displayed on the screen. The two variables reference identical String objects, but not the same one. |
| 6    | `Cat cat1 = new Cat("Oscar"); Cat cat2 = new Cat("Oscar"); System.out.println(cat1.equals(cat2));` | Compare objects. **true** will be displayed on the screen. The two variables reference identical Cat objects |
| 7    | `String s = new String("Mom"); String s2 = new String("Mom"); System.out.println(s.equals(s2));` | Compare objects. **true** will be displayed on the screen. The two variables reference identical String objects |

### 8. Bubble sort

```java
package com.codegym.task.task04.task0420;

/* 
Sorting three numbers

*/

import java.io.*;

public class Solution {
    public static void main(String[] args) throws Exception {
        //write your code here
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        
        int n1 = Integer.parseInt(reader.readLine());
        int n2 = Integer.parseInt(reader.readLine());
        int n3 = Integer.parseInt(reader.readLine());
        
        int[] numbers = {n1,n2,n3};
        boolean sorted = false;
        
        while (!sorted){
            sorted = true;
            for(int i = 0; i <= 1; i++){
                if(numbers[i] < numbers[i+1]){
                    int temp = numbers[i];
                    numbers[i] = numbers[i+1];
                    numbers[i+1] = temp;
                    sorted = false;
                }
            }
        }
        
        for(int i = 0; i <= 2; i++){
            System.out.print(numbers[i] + " ");
        }
        
    }
}

```

### 9. Classes

**OOP**: The programming philosophy that calls for a program to be divided into objects is called object-oriented programming (OOP). Java is a classic example of an OOP language: in Java, everything is an object.

### 10. Packages

Always create classes under packages! When you don't have many classes, this isn't a problem, but when there are many, it's easy to mix them up. Always create classes inside packages.

### 11. Object visibility and null references

```java
Cat cat1 = new Cat("Tommy");
cat1 = null;
```

The object exists as long as at least one variable is storing its address.

"Tommy" exists for one line, on line 2, Tommy is collected by 'garbage collection' performed by JVM.

The garbage collector is an internal Java mechanism responsible for freeing up memory, i.e. removing unnecessary objects from memory.

### 12. Finalize

**Finalize method**: The Java Virtual Machine calls the **finalize**() method before destroying an object. The method is used to deallocate system resources or perform other cleanup tasks. In fact, this method is the exact opposite of a constructor in Java.

### 13. ArrayList

#### 13.1 Why we use ArrayList?

- ArrayList supports several additional operations that programmers have to perform all the time. An oridinary array cannot insert/ delete elements from the middle of an array, but ArrayList can.
- ArrayList is able to change the size of the array

#### 13.2 Generics

Generics are types that have a parameter. When we declare a generic variable, we indicate two types instead of one: the variable type and the type of the data it stores.

e.g. `ArrayList<String> list = new ArrayList<String>();`



### 14. Collection (Important!)

#### 14.1. Intro

**Collection** is a class whose main purpose if to store a collection of other elements.

Three main groups of collection:

- Set: no order
- List: ordered. index
- Map: key value pair. key is unique

https://codegym.cc/quests/lectures/questsyntax.level08.lecture02

#### 14.2 Iterator

Java uses iterator to iterate throught all elements in the collection.

Shorthand version of iterator: for-each statement

```java
public static void main(String[] args)
{
    Set<String> set = new HashSet<String>();
    set.add("Rain");
    set.add("In");
    set.add("Spain");

    for (String text : set)
    {
        System.out.println(text);
    }
}
```

```java
package com.codegym.task.task08.task0802;

/* 
HashMap of 10 pairs

*/

import java.util.HashMap;
import java.util.Map;

public class Solution {
    public static void main(String[] args) throws Exception {
        //write your code here
        HashMap<String, String> strings = new HashMap<String, String>();
        strings.put("watermelon", "melon");
        strings.put("banana", "fruit");
        strings.put("cherry", "fruit");
        strings.put("pear", "fruit");
        strings.put("cantaloupe", "melon");
        strings.put("blackberry", "fruit");
        strings.put("ginseng", "root");
        strings.put("strawberry", "fruit");
        strings.put("iris", "flower");
        strings.put("potato", "tuber");
    
        
        for(Map.Entry<String, String> pair: strings.entrySet()){
            String pairKey = pair.getKey();
            String pairVal = pair.getValue();
            System.out.println(pairKey + " - " + pairVal);
        }

    }
}

```

#### 14.3. List

##### 14.3.1 LinkedList and ArrayList

|                 Description                  |   Operation   | ArrayList | LinkedList |
| :------------------------------------------: | :-----------: | :-------: | :--------: |
|                Get an element                |      get      |   Fast    |    Slow    |
|                Set an element                |      set      |   Fast    |    Slow    |
|   Add an element (to the end of the list)    |      add      |   Fast    |    Fast    |
| Insert an element (at an arbitrary position) | add(i, value) |   Slow    |    Fast    |
|              Remove an element               |    remove     |   Slow    |    Fast    |

if you are going to frequently insert (or remove) elements in the middle of the collection, it's better to use **LinkedList**. In all other cases, **ArrayList** works better.

##### 14.3.2 Get() method

List.get() will return an Integer object, not a primitive int.

So if you'd like to compare two Integer objects, using **equals()**: `list.get(i).equals(list.get(i+1))`

#### 14.4. Set

Group of unordered objects. Unique.

| Operation                            | Method                    |
| ------------------------------------ | ------------------------- |
| Add element(s)                       | add(), addAll()           |
| Remove element(s)                    | remove(), removeAll()     |
| Check for the presence of element(s) | contains(), containsAll() |

##### 14.4.1 Remove() in set

A `Set` has no concept of an index of an element. The elements have no order in the set. Moreover, you should use an `Iterator` when iterating to avoid a [`ConcurrentModificationException`](http://docs.oracle.com/javase/7/docs/api/java/util/ConcurrentModificationException.html) when removing an element from a collection *while* looping over it

```java
package com.codegym.task.task08.task0814;

import java.util.HashSet;
import java.util.*;

/* 
Greater than 10? You're not a good fit for us

*/

public class Solution {
    public static HashSet<Integer> createSet() {
        // write your code here
        HashSet<Integer> numbers = new HashSet<Integer>();
        for(int i = 1; i <= 20; i++){
            numbers.add(i);
        }
        return numbers;
    }

    public static HashSet<Integer> removeAllNumbersGreaterThan10(HashSet<Integer> set) {
        // write your code here
        Iterator<Integer> iterator = set.iterator();
        while(iterator.hasNext()){
          // iterator.next() starts from 1;
            if(iterator.next() > 10){
              // no need to pass in any paramter
                iterator.remove();
            }
        }
        return set;
    }

    public static void main(String[] args) {
       
    }
}

```



#### 14.5. Map

Set of key-value pairs. Unique key.

| Operation                                    | Method               |
| -------------------------------------------- | -------------------- |
| Get a set of all pairs                       | entrySet()           |
| Get a set of all keys                        | keySet()             |
| Get a set of all values                      | values()             |
| Add a pair                                   | put(key, value)      |
| Get the value for the specified key          | get(key)             |
| Check whether the specified key is present   | containsKey(key)     |
| Check whether the specified value is present | containsValue(value) |
| Check whether the Map is empty               | isEmpty()            |
| Clear the Map                                | clear()              |
| Remove the value for the specified key       | remove(key)          |

### 15. Array

#### 15.1 length() vs. length

**array.length :** length is a final variable applicable for[ arrays](https://www.geeksforgeeks.org/arrays-in-java/). With the help of length variable, we can obtain the size of the array.
**string.length() :** length() method is a final variable which is applicable for string objects. length() method returns the number of characters presents in the string.

```java
public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        String s = reader.readLine();

        //write your code here
        String output = "";
       // split string by space
        String[] splitted = s.split("\\s+");
        for(int i = 0; i < splitted.length; i++){
            String word = splitted[i];
            String upperWord = word.substring(0,1).toUpperCase() + word.substring(1);
            splitted[i] = upperWord;
          	// concatenate string by space
            output = String.join(" ", splitted);
        }
        System.out.println(output);
    }
}
```

#### 15.2 Sort numbers and strings

```java
package com.codegym.task.task09.task0930;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.*;

/* 
Task about algorithms

*/

public class Solution {
    public static void main(String[] args) throws Exception {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        ArrayList<String> list = new ArrayList<String>();
        String s = "";
        while (true) {
            s = reader.readLine();

            if (s == "null" || s.isEmpty()) break;
            list.add(s);
        }

        String[] array = list.toArray(new String[list.size()]);
        sort(array);

        for (String x : array) {
            System.out.println(x);
        }
    }

    public static void sort(String[] array) {
        // write your code here
        ArrayList<String> stringList = new ArrayList<String>();
        ArrayList<Integer> numberList = new ArrayList<Integer>();
        
        for(int i = 0; i < array.length; i++){
            if(isNumber(array[i])) numberList.add(Integer.parseInt(array[i]));
            else stringList.add(array[i]);
        }
        
        /* Sorting in decreasing order*/
	   Collections.sort(numberList, Collections.reverseOrder());
	   
	   /* Sorting string list */
        boolean sorted = false;
        
        while(!sorted){
            sorted = true;
            for(int i = 0 ; i < stringList.size() - 1; i++){
                if(isGreaterThan(stringList.get(i), stringList.get(i+1))){
                    Collections.swap(stringList, i, i+1);
                    sorted = false;
                }
            }
        }
        
        // replace the corresponding value in array 
        int numberListIdx = 0;
        int stringListIdx = 0;
        for(int i = 0; i < array.length; i++){
            if(isNumber(array[i])){
                array[i] = Integer.toString(numberList.get(numberListIdx));
                numberListIdx++;
            }else{
                array[i] = stringList.get(stringListIdx);
                stringListIdx++;
            }
        }
        
    }

    // String comparison method: 'a' is greater than 'b'
    public static boolean isGreaterThan(String a, String b) {
        return a.compareTo(b) > 0;
    }


    // Is the passed string a number?
    public static boolean isNumber(String s) {
        if (s.length() == 0) return false;

        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            char c = chars[i];
            if ((i != 0 && c == '-') // The string contains a hyphen
                    || (!Character.isDigit(c) && c != '-') // or is not a number and doesn't start with a hyphen
                    || (i == 0 && c == '-' && chars.length == 1)) // or is a single hyphen
            {
                return false;
            }
        }
        return true;
    }
}

```



### 16. Date

Use calendar 

```java
package com.codegym.task.task08.task0827;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.time.temporal.ChronoUnit;
import java.util.Date;
import java.util.*;

/* 
Working with dates

*/

public class Solution {
    public static void main(String[] args) throws ParseException{
        System.out.println(isDateOdd("MAY 1 2013"));
    }

    public static boolean isDateOdd(String date) throws ParseException{

				// create calendar instance from string
        Calendar checkCal = Calendar.getInstance();
        SimpleDateFormat df = new SimpleDateFormat("MMMM dd yyyy", Locale.ENGLISH);
        checkCal.setTime(df.parse(date));

        Calendar cal = Calendar.getInstance();
        cal.set(Calendar.YEAR, checkCal.get(Calendar.YEAR));
        cal.set(Calendar.DAY_OF_YEAR, 1);
				// calculat the date difference between two calendar objects
        long daysBetween = ChronoUnit.DAYS.between(checkCal.toInstant(), cal.toInstant());
        System.out.println(daysBetween);
        return (daysBetween % 2 != 0);
        
    }
}

```

#### 16.1. Parse date string and format date

```java
package com.codegym.task.task09.task0922;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

/* 
What's today's date?

*/

public class Solution {

    public static void main(String[] args) throws Exception {
        //write your code here
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd", Locale.ENGLISH);
        Date date = df.parse(reader.readLine());
        System.out.println(date);
        SimpleDateFormat formatter = new SimpleDateFormat("MMM dd, YYYY", Locale.ENGLISH);
        String formattedDate = formatter.format(date);
        System.out.println(formattedDate.toUpperCase());
    }
}

```



### 17. Stack 

#### 17.1. Intro

LIFO

- **StackTraceElement**: The Java Machine keeps track of all function calls. For that, it has a special collection – the stack. When one function calls another, the Java Machine puts a new StackTraceElement object onto the stack. When a function finishes, that element is removed from the stack. This means that the stack always stores up-to-date information about the current state of the 'stack of function calls'

  Each StackTraceElement object contains information about the called method. In particular, you can get the method name using the **getMethodName** method.

```java
public class ExceptionExample
{
  public static void main(String[] args)
  {
    method1();
  }

  public static void method1()
  {
    method2();
  }

  public static void method2()
  {
    method3();
  }

  public static void method3()
  {
     StackTraceElement[] stackTraceElements = Thread.currentThread().getStackTrace();
    for (StackTraceElement element : stackTraceElements)
    {
       System.out.println(element.getMethodName());
    }
  }
}
```

### 18. Exception

What happens when an error occurs?

1. When an error occurs, the Java Machine creates a special object – an exception – where it saves all the error information. There are different exceptions for different errors.

2. An exception causes the program to immediately exit the current function, and the next function, and so on – until it exits the main method. Then the program terminates. Programmers may also say that the Java Machine 'unwinds the call stack'."

We can use `try-catch` to catch the exception without terminating the program.

#### 18.1. Checked and Unchecked Exceptions

- checked exceptions: exceptions that are checked at compile time. `e.g. read file, if file does not exist, a FileNotFoundException will be returned (IOException) at compile time`
  - we can handle checked exceptions by **throw** and **try-catch**
- unchecked exceptions: exceptions are not checked at compile time. `e.g. ArithmeticException. even though we have it, we can still compile it. but the errors will be returned at run time.`
  - we often handle unchecked exceptions by **try-catch**

#### 18.2. Exception examples

##### 18.2.1. InterruptedException

if a [`Thread`](http://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html) is sleeping, the thread may be interrupted e.g. with [`Thread.interrupt()`](http://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupt--) by another thread in which case the sleeping thread (the `sleep()` method) will throw an instance of this `InterruptedException`.

```java
package com.codegym.task.task09.task0920;

/* 
Countdown

*/

public class Solution {
    public static void main(String[] args) {
        for (int i = 10; i >= 0; i--) {
            System.out.println(i);

            //write your code here
            try{
                Thread.sleep(100);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}

```

##### 18.2.2. IOException

```java
package com.codegym.task.task09.task0921;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;

import java.io.*;

/* 
Method in a try-catch

*/

public class Solution {
    public static void main(String[] args) {
        readData();
    }

    public static void readData() {
        //write your code here
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        ArrayList<Integer> numbers = new ArrayList<Integer>();
        int num;
        try{
            while(true){
                num = Integer.parseInt(reader.readLine());
                numbers.add(num);
            }
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            
            for(Integer n: numbers){
                System.out.println(n);
            }
        }
    }
}

```

### 19. Type

#### 19.1. Type conversion

- widening primitive type

  ```java
  byte a = 115;
  int b = a;
  ```

- narrowing primitive type: use **cast**

  - **A cast operator** must be put before a number/variable anytime part of the number will be discarded or when a narrowing primitive conversion occurs. The cast operator only affects the number/variable that directly follows it.

  ```java
  int c = 10000;
  byte d = (byte) c;
  ```

**The IEEE has defined certain standards for floating point numbers which include definitions for "Not a Number"(NaN)  and positive and negative infinity. These do not apply to integers. so, the jvm won't throw an exception when double/0 or long/0.0. 

But if it is an integer division it will throw an arithmetic exception.

```java
public class Solution {
    public static void main(String[] args) {
        int a = 0;
        int b = a + 46;
        byte c = (byte) (a * b);
        double f = 1234.15;
        long d = (long) (a + f / c + b);
        System.out.println(d);
    }
}
```

#### 19.2. Object casting

You can assign any reference type to such a variable (**narrowing conversion**). However, to make the assignment in the other direction (**widening conversion**), you must explicitly indicate a cast operation:"

A widening or narrowing reference conversion **doesn't change the object** in any way.

```
// this will cause RUN-TIME ERROR
Object o = 123; // o stores an Integer
Float s2 = (Float) o;

// this works fine
Object o = 123f; // o stores a Float
Float s2 = (Float) o;
```

#### 19.3. Literal

code consists of methods, classes, variables, etc., but literals are specific values written directly in the code