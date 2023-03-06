---
path: '/week-5/2-objects-in-a-list'
title: 'Objects in a list'
hidden: false
---

<text-box variant='learningObjectives' name='Learning Objectives'>

- You can add objects to a list
- You can iterate through objects in a list

</text-box>


The type parameter used to create a list specifies the data type of the elements that will be stored in the list. For example, `List<String>` is used for storing strings, `List<Integer>` for integers, and `List<Double>` for floating-point numbers.

In the following example, we add strings to a list and then print each string that was added to the list.

```java
List<String> names = new ArrayList<>();

// string can first be stored in a variable
String name = "Betty Jennings";
// then add it to the list
names.add(name);

// strings can also be directly added to the list:
names.add("Betty Snyder");
names.add("Frances Spence");
names.add("Kay McNulty");
names.add("Marlyn Wescoff");
names.add("Ruth Lichterman");

// several different repeat statements can be
// used to go through the list elements

// 1. while loop
int index = 0;
while (index < names.size()) {
    System.out.println(names.get(index));
    index = index + 1;
}

System.out.println();
// 2. for loop with index
for (int i = 0; i < names.size(); i++) {
    System.out.println(names.get(i));
}

System.out.println();
// 3. for each loop (no index)
for (String name: names) {
    System.out.println(name);
}
```

<sample-output>

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

</sample-output>

## Adding object to a list

Strings are objects, so it should come as no surprise that other types of objects can also be stored in lists. In the following section, we will take a closer look at how lists can work with objects.

Assuming we have access to the following class definition for a `Person`:

```java
public class Person {

    private String name;
    private int age;
    private int weight;
    private int height;

    public Person(String name) {
        this.name = name;
        this.age = 0;
        this.weight = 0;
        this.height = 0;
    }

    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }

    public void growOlder() {
        this.age = this.age + 1;
    }

    public void setHeight(int newHeight) {
        this.height = newHeight;
    }

    public void setWeight(int newWeight) {
        this.weight = newWeight;
    }

    public double bodyMassIndex() {
        double heightDivByHundred = this.height / 100.0;
        return this.weight / (heightDivByHundred * heightDivByHundred);
    }

    @Override
    public String toString() {
        return this.name + ", age " + this.age + " years";
    }
}
```

Working with objects in a list is very similar to working with any other type of element. The main difference is that you need to specify the type of object that the list will store when you create it.

The example below demonstrates this by first creating a list that will store objects of type `Person`. Then, several `Person` objects are added to the list, and finally, each `Person` object is printed out one by one.

```java
List<Person> persons = new ArrayList<>();

// a person object can be created first
Person john = new Person("John");
// and then added to the list
persons.add(john);

// person objects can also be created "in the same sentence" that they are added to the list
persons.add(new Person("Matthew"));
persons.add(new Person("Martin"));

for (Person person: persons) {
    System.out.println(person);
}
```

<sample-output>

John, age 0 years
Matthew, age 0 years
Martin, age 0 years

</sample-output>

## Adding user-inputted objects to a list

The structure we used earlier for reading inputs is still very useful.

```java
Scanner scanner = new Scanner(System.in);
List<Person> persons = new ArrayList<>();

// Read the names of persons from the user
while (true) {
    System.out.print("Enter a name, empty will stop: ");
    String name = scanner.nextLine();
    if (name.isEmpty()) {
        break;
    }


    // Add to the list a new person
    // whose name is the previous user input
    persons.add(new Person(name));
}

// Print the number of the entered persons, and their individual information
System.out.println();
System.out.println("Persons in total: " + persons.size());
System.out.println("Persons: ");

for (Person person: persons) {
    System.out.println(person);
}
```

<sample-output>

Enter a name, empty will stop: **Alan Kay**
Enter a name, empty will stop: **Ivan Sutherland**
Enter a name, empty will stop: **Kristen Nygaard**

Persons in total: 3
Persons:
Alan Kay, age 0 years
Ivan Sutherland, age 0 years
Kristen Nygaard, age 0 years

</sample-output>

<programming-exercise name='Items'>

Implement the class `Items` described here. **NB!** Don't modify the class `Item`.

Write a program that reads names of items from the user. If the name is empty, the program stops reading. Otherwise, the given name is used to create a new item, which you will then add to the `items` list.

Having read all the names, print all the items by using the `toString` method of the `Item` class. The implementation of the `Item` class keeps track of the time of creation, in addition to the name of the item.

An example of the working program is given below:

<sample-output>

Name: **Hammer**
Name: **Collar**
Name:

Hammer (created at: 06.07.2018 12:34:56)
Collar (created at: 06.07.2018 12:34:57)

</sample-output>

</programming-exercise>
