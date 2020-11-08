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

#### 4.1 Escapting characters

```java
 String windows = "This is a Windows path: \"C:\\Program Files\\Java\\jdk1.8.0_172\\bin\"";
 String javaString = "This is a Javastring:\\\"C:\\\\ProgramFiles\\\\Java\\\\jdk1.8.0_172\\\\bin\\\"";
        System.out.println(windows);
        System.out.println(javaString);
```

This is a Windows path: "C:\Program Files\Java\jdk1.8.0_172\bin" 

This is a Java string: \"C:\\Program Files\\Java\\jdk1.8.0_172\\bin\"

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

- static variables/methods are called on Class
- non-static variables/methods are called on the instance of the class

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

