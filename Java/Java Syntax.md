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

