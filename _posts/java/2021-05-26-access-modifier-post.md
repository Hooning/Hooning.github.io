---
layout: posts
date: 2021-05-26 23:30
title: "[Java] Access Modifier"
categories: basics 
tags: ['java', 'basics']
summary: "What is Access Modifier in Java and how is it used"
permalink: "/java/:title.html"
published: true
---

# What is Access Modifiers? 

Access modifiers are keywords that are generally used in Object-oriented programming languages to set the access scope of classes, fields, constructors, and methods.   

# Why do we need them? 

It enables the concept of encapsulation, which binds the attribute and actions of the object so that it can hide the actual internal implementation. 

# How is it used in Java? 

In Java, there are four types of access modifiers which are public, private, protected, and default (no keyword). 

Firstly, the public modifier enables its access from any level of the code. Secondly, a protected modifier allows access from the same package or child class from another package. Thirdly, in default (also called as package-private) modifier it only allows access from the same package. Lastly, the private modifier provides its access only inside of the same class. 

Above mentioned access levels can be shown in the following table. 

|   Modifier    | Class  | Package  | Subclass  | World  |
|:-------------:|:------:|:--------:|:---------:|:------:|
| public        |  Yes   |   Yes    |    Yes    |  Yes   |
| protected     |  Yes   |   Yes    |    Yes    |   No   |
| No modifier   |  Yes   |   Yes    |    No     |   No   |
| private       |  Yes   |    No    |    No     |   No   |


Let's have a look at example codes for each use case.

Here is an example of POJO (Plain Old Java Object) that describes Person.


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

We have define the `class` as `public` access modifier so that it can be used in other part of the program. Here as a JavaBean standard I have defined all `fields` as `private` access modifier which can only accessed inside of `Person` class. However, we can access them by `public` getter and setter `methods`. 

For constructors, it can be defined as all four types of access modifiers. If you don't define any constructors the compiler will automatically provide a `no-argument constructor` with `public` access modifier. However, if you want to access a no-argument constructor from the **same class** then define the constructor with a `private` access modifier. or to access classes from the **same package** you should explicitly define the Constructor with the `default(package-private)` modifier.

### Case1: protected constructor
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
  } 

} 
```

Here we defined `protected` constructor in `Vehicle(parent)` class and then defined `Sedan(sub)` Class. Even both classes are in different packages Sedan class can send the argument to the Vehicle constructor.

### Case2: default constructor
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
  } 

} 
```

Here we defined the `default(package-private)` constructor in the `Vehicle` class and used it to instantiate it from the `Bus` class which is in the same package.

### Case3: private constructor (Singleton example)
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
  } 

} 
```

Here we defined a `private` constructor in the Vehicle class. In a normal case, it prevents being instantiated out of its class. However, the above example shows the common pattern of `Singleton`, where it uses the `public static factory method` that calls its own `private` constructor.


