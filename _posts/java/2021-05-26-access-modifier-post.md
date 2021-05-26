---
layout: posts
date: 2021-05-26 23:30
title: "[Java] Access Modifier"
categories: basics 
tags: ['java', 'basics']
summary: "What is Access Modifier in Java and how is it used"
permalink: "/java/:title.html"
published: false
---

# What? 

Access modifiers are keywords that are generally used in Object-oriented programming languages to set the access scope of classes, fields, constructors, and methods.   

# Why? 

It enables the concept of encapsulation, which binds the attribute and actions of the object so that it can hide the actual internal implementation. 

# How? 

In Java, there are four types of access modifiers which are public, private, protected, and default (no keyword). 

Firstly, the public modifier enables its access from any level of the code. Secondly, a protected modifier allows access from the same package or child class from another package. Thirdly, in default (also called as package-private) modifier it only allows access from the same package. Lastly, the private modifier provides its access only inside of the same class. 

Above mentioned access levels can be shown in the following table. 

|   Modifier    | Class  | Package  | Subclass  | World  |
|:-------------:|:------:|:--------:|:---------:|:------:|
| public        |  Yes   |   Yes    |    Yes    |  Yes   |
| protected     |  Yes   |   Yes    |    Yes    |   No   |
| No modifier   |  Yes   |   Yes    |    No     |   No   |
| private       |  Yes   |    No    |    No     |   No   |


<br/>
Let's have a look at example codes for each use case.
<br/><br/>
Here is an example of POJO (Plain Old Java Object) that describes Person.
<br/><br/>

```java
public class Person {

  // fields
  private String firstName;
  private String lastName;
  private LocalDate birthDate;

  // constructor
  public Person(String firstName, String lastName, LocalDate birthDate) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.gender = gender;
    this.birthDate = birthDate;
  }

  /* getter and setter methods*/
  public String getFirstName() {
    return firstName;
  }

  public void setFirstName(String firstName) {
    this.firstName = firstName;
  }
  ...

}
```

We have define the `class` as `public` access modifier so that it can be used in other part of the program. Here as a JavaBean standard I have defined all `fields` as `private` access modifier which can only accessed inside of Person class. However, we can access them by `public` getter and setter `methods`. 

For constructors, it can be defined as all four types of access modifiers. If you don't define any constructors the compiler will automatically provide a `no-argument constructor` with `public` access modifier. However, if you want to access a no-argument Constructor from the `same class` then define the Constructor with a `private` access modifier. or to access classes from the `same package` you should explicitly define the Constructor with the `default(package-private)` modifier.

<br/>

### Case1: protected constructor
<br/>

```java
package package1;  

public class Vehicle {

  private int wheelCount; 

  // protected constructor
  protected Vehicle(int wheelCount) { 
    this.wheelCount = wheelCount; 
  }  

  public int getWheelCount() { 
    return wheelCount; 
  } 

  public void setWheelCount(int wheelCount) { 
    this.wheelCount = wheelCount; 
  } 

} 

/* ===== Sedan class ===== */  
package package2; 

import package1.Vehicle; 

public class Sedan extends Vehicle { 
  public Sedan(int wheelCount) { 
    super(wheelCount); 
  } 

  public static void main(String[] args) { 
    Vehicle vehicle = new Sedan(4); 
    System.out.println("Sedan wheel count: " + vehicle.getWheelCount()); 
  } 

} 
```

Here we defined `protected` constructor in `Vehicle(parent)` class and then defined `Sedan(sub)` Class. Even both classes are in different packages Sedan class can send the argument to the Vehicle constructor.

Output: 
```
Sedan wheel count: 4
```

<br/>

### Case2: default constructor
<br/>

```java
package package1; 

public class Vehicle { 

  private int wheelCount; 

  // [case2] No modifier(package-private) 
  Vehicle(int wheelCount) { 
    this.wheelCount = wheelCount; 
  } 

  public int getWheelCount() { 
    return wheelCount; 
  } 

  public void setWheelCount(int wheelCount) { 
    this.wheelCount = wheelCount; 
  }  

}   

/* ===== Bus class ===== */
package package1; 

public class Bus {  

  public static void main(String[] args) { 
    Vehicle vehicle = new Vehicle(6); 
    System.out.println("Bus wheel count: " + vehicle.getWheelCount()); 
  } 

} 
```

Here we defined the `default(package-private)` constructor in the `Vehicle` class and used it to instantiate it from the `Bus` class which is in the same package.

Output:
```
Bus wheel count: 6
```

<br/>

### Case3: private constructor (Singleton example)
<br/>

```java
package package1; 

public class Vehicle {

  private int wheelCount;

  // [case3] Singleton example
  private static final Vehicle uniqueInstance = new Vehicle(); 

  // private constructor
  private Vehicle() {} 

  public static Vehicle getInstance(){ 
    return uniqueInstance; 
  }

  public int getWheelCount() { 
    return wheelCount; 
  }

  public void setWheelCount(int wheelCount) { 
    this.wheelCount = wheelCount; 
  } 

} 

/* ===== Truck class ===== */   
package package2; 

import package1.Vehicle; 

public class Truck { 

  public static void main(String[] args) {
    Vehicle vehicle = Vehicle.getInstance(); 
    vehicle.setWheelCount(12); 
    System.out.println("Truck wheel count: " + vehicle.getWheelCount()); 
  } 

} 
```

Here we defined a `private` constructor in the Vehicle class. In a normal case, it prevents being instantiated out of its class. However, the above example shows the common pattern of `Singleton`, where it uses the `public static factory method` that calls its own `private` constructor.

Output:
```
Truck wheel count: 12
```

