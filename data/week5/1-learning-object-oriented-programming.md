---
path: '/week-5/1-learning-object-oriented-programming'
title: 'Learning object-oriented programming'
hidden: false
---

<text-box variant='learningObjectives' name='Learning Objectives'>

- To revise the concepts of class and object.
- To realize that a program that has been written without objects can also be written using objects.
- To realize that the use of objects can make a program more understandable.

</text-box>

Let's take a moment to explore the concept of object-oriented programming.

To understand it better, let's consider a clock. A clock typically has three hands: hours, minutes, and seconds. The second-hand advances once every second, the minute hand advances every sixty seconds, and the hour hand advances every sixty minutes. When the second-hand reaches a value of 60, it is reset to zero and the minute hand advances by one. Similarly, when the minute hand reaches a value of 60, it is reset to zero and the hour hand advances by one. When the hour hand reaches a value of 24, it is reset to zero.

The time is usually displayed in the format `hours:minutes:seconds`, where two digits are used to represent each component of the time.

In the example below, the clock has been implemented using integer variables. (Note that the printing could be handled in a separate method, but for simplicity, it is included within the code.)

```java
int hours = 0;
int minutes = 0;
int seconds = 0;

while (true) {
    // 1. Printing the time
    if (hours < 10) {
        System.out.print("0");
    }
    System.out.print(hours);

    System.out.print(":");

    if (minutes < 10) {
        System.out.print("0");
    }
    System.out.print(minutes);

    System.out.print(":");

    if (seconds < 10) {
        System.out.print("0");
    }
    System.out.print(seconds);
    System.out.println();

    // 2. The second hand's progress
    seconds = seconds + 1;

    // 3. The other hand's progress when necessary
    if (seconds > 59) {
        minutes = minutes + 1;
        seconds = 0;

        if (minutes > 59) {
            hours = hours + 1;
            minutes = 0;

            if (hours > 23) {
                hours = 0;
            }
        }
    }
}
```

As we can see in the example above, the working of a clock consisting of three `int` variables is not necessarily clear to someone reading the code. By looking at the code namely, it's difficult to "see" what's going on. A famous <a href="https://en.wikipedia.org/wiki/Kent_Beck" target="_blank" rel="noopener"> programmer </a> once remarked *"Any fool can write code that a computer can understand. Good Programmers write code that humans can understand"*.

<br/>

In order to enhance the clarity of the program, we can transform the concept of a clock hand into its own distinct class. This will provide a clear and organized way to handle the behavior of clock hands.

To accomplish this, we can create a `ClockHand` class that defines the properties of a clock hand, including its current value and upper limit (i.e., the value at which the hand resets to zero). Additionally, we can create methods within the class for advancing the hand, retrieving its current value, and printing the value in string form.

By encapsulating the behavior of a clock hand within its own class, the overall program will become more intuitive and easier to understand. Below is an example implementation of the `ClockHand` class.

```java
public class ClockHand {
    private int value;
    private int limit;

    public ClockHand(int limit) {
        this.limit = limit;
        this.value = 0;
    }

    public void advance() {
        this.value = this.value + 1;

        if (this.value >= this.limit) {
            this.value = 0;
        }
    }

    public int value() {
        return this.value;
    }

    public String toString() {
        if (this.value < 10) {
            return "0" + this.value;
        }

        return "" + this.value;
    }
}
```

By creating the `ClockHand` class, the behavior of the clock has become much clearer. We can now easily print the clock hand, while the hand's progression is handled internally by the `ClockHand` class.

In contrast to the previous implementation that used integers to represent the clock hands, the use of clock-hand objects changes the way the hands work together. The `ClockHand` class includes an upper-limit variable that automatically resets the hand to zero once it reaches the upper limit. As a result, the minute hand advances only when the second hand's value is zero, and the hour hand advances only when the minute hand's value is zero.

Overall, this new approach provides a clearer and more intuitive way to represent the behavior of a clock. The following code demonstrates the updated `ClockHand` class in action.

```java
ClockHand hours = new ClockHand(24);
ClockHand minutes = new ClockHand(60);
ClockHand seconds = new ClockHand(60);

while (true) {
    // 1. Printing the time
    System.out.println(hours + ":" + minutes + ":" + seconds);

    // 2. Advancing the second hand
    seconds.advance();

    // 3. Advancing the other hands when required
    if (seconds.value() == 0) {
        minutes.advance();

        if (minutes.value() == 0) {
            hours.advance();
        }
    }
}
```

**Object-oriented programming is fundamentally about separating concepts into distinct entities, or in other words, creating abstractions.** Despite the previous example, one might question the value of creating an object that contains only a number, since the same could be achieved with `int` variables. However, there are many reasons why separating a concept into its own class is beneficial.

Firstly, the details of a concept can be hidden or abstracted within the class. For instance, the rotation of a clock hand can be handled by a clearly named method such as `advance()`, rather than requiring an if-statement and assignment operation each time the hand needs to be moved. Furthermore, a class created to represent a distinct concept, such as a clock hand, can be reused in other programs and given a new name such as `CounterLimitedFromTop`.

Another significant advantage of using classes is that the implementation details of a class can be changed without affecting the external interface or behavior of the class. This allows for greater flexibility and easier maintenance of code.

In the case of a clock, there are three distinct hands, each representing a separate concept. By creating a class to represent the clock, we can encapsulate the hands within it and provide a simpler and more intuitive interface to the user. Thus, we can create a class called `Clock` that hides the hands inside it.

Overall, by separating related concepts into their own classes, we can create more modular, reusable, and maintainable code. Below is an example implementation of the `Clock` class.



```java
public class Clock {
    private ClockHand hours;
    private ClockHand minutes;
    private ClockHand seconds;

    public Clock() {
        this.hours = new ClockHand(24);
        this.minutes = new ClockHand(60);
        this.seconds = new ClockHand(60);
    }

    public void advance() {
        this.seconds.advance();

        if (this.seconds.value() == 0) {
            this.minutes.advance();

            if (this.minutes.value() == 0) {
                this.hours.advance();
            }
        }
    }

    public String toString() {
        return hours + ":" + minutes + ":" + seconds;
    }
}
```

This way the functions in the program have become increasingly clearer. When you compare our program below to the original one, which used only integers as variables, you'll find that the program's readability is superior.

```java
Clock clock = new Clock();

while (true) {
    System.out.println(clock);
    clock.advance();
}
```

The clock we implemented above is a prime example of an object that relies on "simpler" objects, namely its hands, for its functionality. This is the fundamental principle of object-oriented programming: building programs from small, distinct objects that collaborate with one another.


<programming-exercise name='One Minute'>

Implement a new `Timer` class based on the `Clock` class provided above. The timer should have two hands, one for hundredths of a second and one for seconds. As the timer progresses, the number of hundredths of a second should increase by one. Once the hundredths hand reaches a value of 100, it should be reset to zero, and the seconds hand should increase by one. Similarly, when the seconds hand reaches a value of 60, it should be reset to zero.

The `Timer` class should have the following methods:

- `public Timer()`: creates a new timer.
- `public String toString()`: returns a string representation of the timer in the format "seconds: hundredths of a second", where both the seconds and the hundredths of a second are represented by two numbers. For example, "19:83" would represent the time 19 seconds, 83 hundredths of a second.
- `public void advance()`: moves the timer forward by a hundredth of a second.
You can test the timer's functionality in the main program provided. The program prints the timer and advances it once every hundredth of a second. Once you've finished implementing the `Timer` class, please return the value.

```java
Timer timer = new Timer();

while (true) {
    System.out.println(timer);
    timer.advance();

    try {
        Thread.sleep(10);
    } catch (Exception e) {

    }
}
```

NB! The program above will never stop running by itself. Press the red square to the left of the program's print window to turn it off.

</programming-exercise>

Next, let's review topic terminology.

## Object

An Object is an entity that contains data (instance variables) and behavior (methods) and can take various forms. Objects interact with each other through method calls to request information or give instructions. Each object has its own clearly defined boundaries and behaviors, and is only aware of other objects it needs to perform its tasks. The object hides its internal operations, providing access to its functionality through defined methods, and is independent of any other object it doesn't require to accomplish its task.

In the previous section, we used a "Person" class to define the blueprint for creating person objects, which had properties such as name, age, weight, and height, as well as methods. More variables related to a person, such as personal ID number, telephone number, address, and eye color, could also be added to the person object.

When building an application that deals with people, the functionality and features related to a person are gathered based on the application's use case. For example, an application focused on personal health and well-being would likely track age, weight, height, and provide tools to calculate body mass index and maximum heart rate. In contrast, an application focused on communication would store people's email addresses and phone numbers, but would have no need for weight or height information.

An object's state refers to the value of its internal variables at any given point in time.

In the Java programming language, a Person object that keeps track of name, age, weight, and height, and provides the ability to calculate body mass index and maximum heart rate would look like the following. Below, the height and weight are expressed as doubles - the unit of length is one meter.

```java
public class Person {
    private String name;
    private int age;
    private double weight;
    private double height;

    public Person(String name, int age, double weight, double height) {
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.height = height;
    }

    public double bodyMassIndex() {
        return this.weight / (this.height * this.height);
    }

    public double maximumHeartRate() {
        return 206.3 - (0.711 * this.age);
    }

    public String toString() {
        return this.name + ", BMI: " + this.bodyMassIndex()
            + ", maximum heart rate: " + this.maximumHeartRate();
    }
}
```

```java
Scanner reader = new Scanner(System.in);
System.out.println("What's your name?");
String name = reader.nextLine();
System.out.println("What's your age?");
int age = Integer.valueOf(reader.nextLine());
System.out.println("What's your weight?");
double weight = Double.valueOf(reader.nextLine());
System.out.println("What's your height?");
double height = Double.valueOf(reader.nextLine());

Person person = new Person(name, age, weight, height);
System.out.println(person);
```

<sample-output>

What's your name?
**Napoleone Buonaparte**
What's your age
**51**
What's your weight?
**80**
What's your height?
**1.70**
Napoleone Buonaparte, BMI: 27.68166089965398, maximum heart rate: 170.03900000000002

</sample-output>

## Class

A class serves as a blueprint for creating objects. It includes instance variables that define the data of an object, a constructor or constructors used to create it, and methods that define its behavior. Below is an example of a rectangle class that provides the functionality of a rectangle.

```java
// class
public class Rectangle {

    // instance variables
    private int width;
    private int height;

    // constructor
    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    // methods
    public void widen() {
        this.width = this.width + 1;
    }

    public void narrow() {
        if (this.width > 0) {
            this.width = this.width - 1;
        }
    }

    public int surfaceArea() {
        return this.width * this.height;
    }

    public String toString() {
        return "(" + this.width + ", " + this.height + ")";
    }
}
```

The class presented above contains methods that return a value, as well as methods that do not return a value (indicated by the keyword `void` in their definition). The class also provides a `toString` method which returns a string representation of the object.

To create objects from the class, we use the `new` command with the appropriate constructor. In the example below, we create two rectangle objects and display information about them.

```java
Rectangle first = new Rectangle(40, 80);
Rectangle rectangle = new Rectangle(10, 10);
System.out.println(first);
System.out.println(rectangle);

first.narrow();
System.out.println(first);
System.out.println(first.surfaceArea());
```

<sample-output>

(40, 80)
(10, 10)
(39, 80)
3920

</sample-output>

<programming-exercise name='Book'>

Create a "Book" class that describes a book. Each book has an author, title, and page count.

In this class, make a:

- Constructor `public Book(String author, String name, int pages)`
- Method `public String getAuthor()` that returns the book's author's name.
- Method `public String getName()` that returns the name of the book.
- Method `public int getPages()` that returns the number of pages in the book.

In addition, make a `public String toString()` method for the book that will be used to print the book object. For example, the method call should produce the following output:

<sample-output>

<!-- J. K. Rowling, Harry Potter ja viisasten kivi, 223 sivua -->
J. K. Rowling, Harry Potter and the Sorcerer's Stone, 223 pages

</sample-output>

</programming-exercise>

<programming-exercise name='Fitbyte'>


<a href="https://en.wikipedia.org/wiki/Heart_rate#Karvonen_method" target="_blank" norel>The Karvonen method </a> allows you to calculate your target heart rate for physical exercise. The target heart rate is calculated with the formula `(maximum heart rate - resting heart rate) * (target heart rate percentage) + resting heart rate`, where the target heart rate is given as a percentage of the maximum heart rate.

For example, if a person has a maximum heart rate of `200`, a resting heart rate of `50`, and a target heart rate of `75%` of the maximum heart rate, the target heart rate should be about `((200-50) * (0.75) + 50)`, i.e., `162.5` beats per minute.

Create a class called `Fitbyte`. Its constructor takes both the age and resting heart rate as its parameters. The exercise assistant should provide a method targetHeartRate, which is passed a number of type `double` as a parameter that represents a percentual portion of the maximum heart rate. The proportion is given as a number between zero and one. The class should have:

- A constructor `public Fitbyte(int age, int restingHeartRate)`
- A method `public double targetHeartRate(double percentageOfMaximum)` that calculates and returns the target heart rate.


Use the `206.3 - (0.711 * age)` formula to calculate the maximum heart rate.

Use case:

```java
Fitbyte assistant = new Fitbyte(30, 60);

double percentage = 0.5;

while (percentage < 1.0) {
    double target = assistant.targetHeartRate(percentage);
    System.out.println("Target " + (percentage * 100) + "% of maximum: " + target);
    percentage = percentage + 0.1;
}
```

<sample-output>
<!--
Tavoite 50.0% maksimista: 122.48500000000001
Tavoite 60.0% maksimista: 134.98200000000003
Tavoite 70.0% maksimista: 147.479
Tavoite 80.0% maksimista: 159.976
Tavoite 89.99999999999999% maksimista: 172.473
Tavoite 99.99999999999999% maksimista: 184.97000000000003 -->

Target 50.0% of maximum: 122.48500000000001
Target 60.0% of maximum: 134.98200000000003
Target 70.0% of maximum: 147.479
Target 80.0% of maximum: 159,976
Target 89.99999999999999% of maximum: 172.473
Target 99.99999999999999% of maximum: 184.97000000000003

</sample-output>

</programming-exercise>
