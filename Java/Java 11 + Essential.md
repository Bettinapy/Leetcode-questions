# Java11 + Essentials

### 1. What is Java

#### 1.1 What is Java Architecture

- Java code is converted into byte codes which is done by the Java Compiler
- The byte codes are coverted into machine code by JVM (Java Virtual Machine)
- The machine code is executed directly by the machine

https://www.edureka.co/blog/java-architecture/

### 2. Variables

primitive wrapper class `e.g. byte => Byte`

you can call some methods on the wrapper class `e.g. Double.parseDouble()`

#### 2.1 Inferred Variable

The role of `var` in a local variable declaration is to stand in for the type, so that the name and initializer stand out: `var person = new Person();` The compiler infers the type of the local variable from the initializer. This is especially worthwhile if the type is parameterized with wildcards, or if the type is mentioned in the initializer. Using `var` can make code more concise without sacrificing readability, and in some cases it can improve readability by removing redundancy.