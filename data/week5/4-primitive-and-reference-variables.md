---
path: '/week-5/4-primitive-and-reference-variables'
title: 'Primitive and reference variables'
hidden: false
---

<text-box variant='learningObjectives' name='Learning Objectives'>

- You understand the terms primitive and reference variable.
- You know the types of primitive variables in Java, and also that there can practically be an infinite number of different reference variables.
- You know the differences in behavior between primitive and reference variables when values are assigned to them, or when they are used as method parameters.

</text-box>

Variables in Java can be classified into two types: primitive and reference variables. A primitive variable's value is stored directly in the variable, while a reference variable holds a reference to an object.

To illustrate the difference between these two types, let's consider two examples.

```java
int value = 10;
System.out.println(value);
```

<sample-output>

10

</sample-output>

```java
public class Name {
    private String name;

    public Name(String name) {
        this.name = name;
    }
}
```

```java
Name luke = new Name("Luke");
System.out.println(luke);
```

<sample-output>

Name@4aa298b7

</sample-output>

In the first example, we declare a variable of primitive type `int` and assign the value of `10` to it. When we pass this variable as an argument to the `System.out.println` method, the output will be the number `10`.

In the second example, we declare a variable of reference type called `luke`. When we create an instance of the `Name` class using its constructor and assign the reference to the `luke` variable, we get a string representation of the object's memory address when we try to print `luke`. This is because a reference variable stores the address of the object it refers to, rather than the object itself. Therefore, when we print `luke`, we get a string representation of the memory location where the object is stored, in the format `Name@4aa298b7`.

This default behavior of printing memory addresses can be overridden by defining a `toString` method in the class of the object we want to print. The `toString` method should return a string representation of the object that we want to print. In the following example, we have defined a `public String toString()` method in the `Name` class, which returns the value of the instance variable name. Now, when we call `System.out.println` on an instance of the `Name` class, it will print the string representation returned by the `toString` method.

```java
public class Name {
    private String name;

    public Name(String name) {
        this.name = name;
    }

    public String toString() {
        return this.name;
    }
}
```

```java
Name luke = new Name("Luke");
System.out.println(luke); // equal to System.out.println(luke.toString());
```

<sample-output>

Luke

</sample-output>

## Primitive Variables

Java provides eight different primitive variable types, including `boolean`, `byte`, `char`, `short`, `int`, `long`, `float`, and `double`. Each of these types has a specific range of values that it can store.

The `boolean` type stores a truth value, which can be either `true` or `false`. The `byte` type is an 8-bit signed integer that can hold values between -128 and 127. The `char` type is a 16-bit Unicode character that can represent a single character. The `short` type is a 16-bit signed integer that can hold values between -32768 and 32767. The `int` type is a 32-bit signed integer that can hold values between -2^31 and 2^31-1. The `long` type is a 64-bit signed integer that can hold values between -2^63 and 2^63-1. The `float` type is a 32-bit floating-point number that can represent a wide range of values. The `double` type is a 64-bit floating-point number that can represent an even wider range of values than `float`.

In our programming, we have been mainly using the `boolean` type for storing truth values, the `int` type for storing medium-sized integers, and the `double` type for storing floating-point numbers. However, depending on the requirements of the program, we may use other variable types as well.

```java
boolean truthValue = false;
int integer = 42;
double floatingPointNumber = 4.2;

System.out.println(truthValue);
System.out.println(integer);
System.out.println(floatingPointNumber);
```

<sample-output>

false
42
4.2

</sample-output>

When we declare a primitive variable in Java, the computer allocates a portion of memory to store the value assigned to that variable. The size of the memory allocated depends on the type of the primitive variable.
In the example provided, we create three primitive variables. Each variable is assigned a value, and the computer reserves a memory location to store that value. The size of each memory location depends on the type of the variable.

```java
int first = 10;
int second = first;
int third = second;
System.out.println(first + " " + second + " " + third);
second = 5;
System.out.println(first + " " + second + " " + third);
```

```java
10 10 10
10 5 10
```

The name of the variable tells the memory location where its value is stored. When you assign a value to a primitive variable with an equality sign, the value on the right side is copied to the memory location indicated by the name of the variable. For example, the statement `int first = 10` reserves a location called `first` for the variable, and then copies the value `10` into it.

Similarly, the statement `int second = first;` reserves in memory a location called `second` for the variable being created and then copies into it the value stored in the location of variable `first`.

It's important to note that when a variable is used as a parameter in a method call, its value is also copied. This means that the value of the variable passed as a parameter during the method call is not mutated in the calling method by the called method. In the example below, we declare a `number` variable in the `main` method whose value is copied as the method call's parameter. In the called method, the value that comes through the parameter is printed, its value is then incremented by one. The value of the variable is then printed once more, and the program execution finally returns to the `main` method. The value of the `number` variable in the `main` method remains unaltered because it has nothing to do with the `number` variable defined as the parameter of the called method.

<code-states-visualizer input='{"code":"public class Example {\n    public static void main(String[] args) {\n        int number = 1;\n        call(number);\n       \n        System.out.println(\"Number still: \" + number);\n    }\n   \n    public static void call(int number) {\n        System.out.println(\"Number in the beginning: \" + number);\n        number = number + 1;\n        System.out.println(\"Number in the end: \" + number);\n    }\n}","stdin":"","trace":[{"stdout":"","event":"call","line":3,"stack_to_render":[{"func_name":"main:3","encoded_locals":{},"ordered_varnames":[],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"1","frame_id":1}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":3,"stack_to_render":[{"func_name":"main:3","encoded_locals":{},"ordered_varnames":[],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"2","frame_id":2}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"step_line","line":4,"stack_to_render":[{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"4","frame_id":4}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"","event":"call","line":10,"stack_to_render":[{"func_name":"call:10","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"7","frame_id":7},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"8","frame_id":8}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"","event":"step_line","line":10,"stack_to_render":[{"func_name":"call:10","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"9","frame_id":9},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"10","frame_id":10}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"Number in the beginning: 1\n","event":"step_line","line":11,"stack_to_render":[{"func_name":"call:11","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"15","frame_id":15},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"16","frame_id":16}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"Number in the beginning: 1\n","event":"step_line","line":12,"stack_to_render":[{"func_name":"call:12","encoded_locals":{"number":2},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"17","frame_id":17},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"18","frame_id":18}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"Number in the beginning: 1\nNumber in the end: 2\n","event":"step_line","line":13,"stack_to_render":[{"func_name":"call:13","encoded_locals":{"number":2},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"27","frame_id":27},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"28","frame_id":28}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"Number in the beginning: 1\nNumber in the end: 2\n","event":"return","line":13,"stack_to_render":[{"func_name":"call:13","encoded_locals":{"number":2,"__return__":["VOID"]},"ordered_varnames":["number","__return__"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"29","frame_id":29},{"func_name":"main:4","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":false,"is_zombie":false,"is_parent":false,"unique_hash":"30","frame_id":30}],"globals":{},"ordered_globals":[],"func_name":"call","heap":{}},{"stdout":"Number in the beginning: 1\nNumber in the end: 2\n","event":"step_line","line":6,"stack_to_render":[{"func_name":"main:6","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"31","frame_id":31}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"Number in the beginning: 1\nNumber in the end: 2\nNumber still: 1\n","event":"step_line","line":7,"stack_to_render":[{"func_name":"main:7","encoded_locals":{"number":1},"ordered_varnames":["number"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"36","frame_id":36}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}},{"stdout":"Number in the beginning: 1\nNumber in the end: 2\nNumber still: 1\n","event":"return","line":7,"stack_to_render":[{"func_name":"main:7","encoded_locals":{"number":1,"__return__":["VOID"]},"ordered_varnames":["number","__return__"],"parent_frame_id_list":[],"is_highlighted":true,"is_zombie":false,"is_parent":false,"unique_hash":"37","frame_id":37}],"globals":{},"ordered_globals":[],"func_name":"main","heap":{}}],"userlog":"Debugger VM maxMemory: 455M\n"}'></code-states-visualizer>

## Reference Variables

All variables in Java, except for the eight primitive variables mentioned previously, are of reference type. In addition, programmers can define their own variable types by creating new classes. When an object is created from a class, it is always a reference variable.

Let's look at the example from the beginning of the chapter where we created a variable called `leevi` of type `Name`.

```java
Name leevi = new Name("Leevi");
```

The call has the following parts:

- Whenever a new variable is declared, its type must be stated first. In the example below, we declare a variable of type `Name`. In order for the program to execute correctly, there must be a `Name` class defined and available for the program to use.

```java
Name ...
```

- We state the name of the variable as it is declared. You can reference the value of the variable later on by its name. Below, the variable name is defined as `leevi`.

```java
Name leevi...
```

- Variables hold values, and objects are created from classes by calling the class constructor. The constructor defines the initial values assigned to the instance variables of the object being created. In the example below, we assume that the `Name` class has a constructor that takes a string as a parameter.

```java
... new Name("Leevi");
```

- The process of creating a new object from a class involves calling the class constructor, which defines the initial values for the instance variables of the object. The constructor call returns a reference to the newly-created object. To assign this reference to a variable, we use the equality sign, which copies the value of the right-hand side expression as the value of the left-hand side variable. In the example below, the value of the variable `leevi` is assigned the reference to the newly-created `Person` object, returned by the constructor call.

```java
Name leevi = new Name("Leevi");
```

The difference between primitive and reference variables is significant. The primary difference is that primitive variables, which are usually numbers, are immutable, while reference variables' internal state can usually be changed. This is because the value of a primitive variable is stored directly in the variable, whereas the value of a reference variable is a reference to the variable's data, or its internal state.

Arithmetic operations such as addition, subtraction, and multiplication can be performed on primitive variables without changing their original values. These operations create new values that can be stored in variables as needed. In contrast, the values of reference variables cannot be changed by these arithmetic expressions.

A reference variable's value, which is the reference itself, points to a location containing information about the variable. Suppose we have a Person class with an instance variable called "age." If we instantiate a person object from the class, we can access the age variable by following the object's reference. Then we can change the value of the age variable as required.

## Primitive and Reference Variable as Method Parameters

As previously mentioned, primitive variables store their values directly, while reference variables hold a reference to an object. When we assign a value using the equality sign, the value on the right-hand side is copied and stored as the value of the left-hand side variable.

During a method call, a similar copying process occurs for both primitive and reference variables. The value of the variable is passed to the method as an argument and copied for the method to use. For primitive variables, the value is conveyed to the method, while for reference variables, the reference is passed as a value.

Let's look at this in practice and assume that we have the following `Person` class available to us.

```java
public class Person {
    private String name;
    private int birthYear;

    public Person(String name) {
        this.name = name;
        this.birthYear = 1970;
    }

    public int getBirthYear() {
        return this.birthYear;
    }

    public void setBirthYear(int birthYear) {
        this.birthYear = birthYear;
    }

    public String toString() {
        return this.name + " (" + this.birthYear + ")";
    }
}
```

We'll inspect the execution of the program step by step.

```java
public class Example {
    public static void main(String[] args) {
        Person first = new Person("First");

        System.out.println(first);
        youthen(first);
        System.out.println(first);

        Person second = first;
        youthen(second);

        System.out.println(first);
    }

    public static void youthen(Person person) {
        person.setBirthYear(person.getBirthYear() + 1);
    }
}
```

<sample-output>

First (1970)
First (1971)
First (1972)

</sample-output>

The program begins its execution from the first line of the main method, where a variable of type `Person` is declared. The value returned by calling the constructor of the `Person` class is then copied as the value of the variable. This constructor creates a new object with a birth year of 1970 and a name set to the value received as a parameter. As usual, the constructor returns a reference to the newly-created object. After executing this line, the program's state is such that a `Person` object has been created in memory, and the `first` variable declared in the main method holds a reference to it.

*In the illustrations below, the call stack is on the left-hand side, and the memory of the program on the right.


<img src="../img/drawings/part5.3-first-1-tm.png"/>

On the third line of the main method, the value of the `first` variable is printed using the `System.out.println` method. This method searches for the `toString` method on the object referenced by the `first` variable. Since the `Person` class has its own `toString` method, that method is called on the object referenced by `first`. The `name` variable in that object has the value "First", and the `birthYear` variable has the value 1970, so the output becomes "First (1970)".

On the fourth line, the `youthen` method is called with the `first` variable passed as an argument. When the `youthen` method is called, the value of the `first` variable is copied and passed as a parameter to the `youthen` method. The execution of the `main` method waits in the call stack. Since the `first` variable is a reference type, the reference to the object created earlier is copied for the method to use. At the end of the `youthen` method execution, the birth year of the object referenced by the `first` variable is incremented by one.


<img src="../img/drawings/part5.3-first-2-tm.png"/>

When the execution of the method `makeYounger` ends, we return back to the `main` method. The information related to the execution of the `makeYounger` disappears from the call stack.

<img src="../img/drawings/part5.3-first-3-tm.png"/>


Once we return from the method call, we print the value of the variable `first` again. During the `youthen` method call, the object referenced by the variable `first` was mutated, with the `birthYear` variable being incremented by one. As a result, the final value printed is "First (1971)".

Next, a new variable of type `Person`, called `second`, is declared in the program. The value of the variable `first` is copied to the variable `second`, meaning that the value of `second` becomes a reference to the same existing `Person` object.

<img src="../img/drawings/part5.3-first-4-tm.png"/>

After this, the program passes the `second` variable as a parameter to the `youthen` method. Similar to before, the reference contained in `second` is copied as the value of the parameter variable for the method's use. After the method's execution, the birth year of the object referenced by the method has once again increased by one.

<img src="../img/drawings/part5.3-first-5-tm.png"/>

Finally, the method execution ends, and the program returns to the main method where the value of the variable `first` is printed one more time. The final result of the print is "First(1972)".


<text-box variant='hint' name='Variables and Computer Memory'>

Whilst discussing the concept of variables and computer memory, it's important to note that the course material provides a simplified version of the topic. This level of abstraction is suitable for learning programming, but from an operating system perspective, a lot more happens when a statement like `int number = 5` is executed.

Specifically, when this statement is executed, two lockers in memory are reserved: one for the value `5` and another for the variable `number`. The size of the location is determined by the type of variable in question. After this reservation is made, the contents of the memory location storing the value `5` are then copied into the memory location reserved for the `number` variable.

Moreover, it's worth mentioning that the `number` variable is not technically a memory location or container. Rather, the value of the `number` variable is an address in memory, with the type of variable providing information about how much data should be retrieved from that address. For example, for an integer, this value would typically be 32 bits.

</text-box>
