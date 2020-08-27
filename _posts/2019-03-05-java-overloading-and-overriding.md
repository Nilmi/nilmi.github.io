---
layout: post
title:  "Overriding vs Overloading in Java"
date:   2019-03-05 22:15:30 +0800
categories: Java
---
<p>Overloading and Overriding, even though these two words seems pretty similar there is a big difference in terms of how to use, when to use, programming rule. This article describes about both of these concepts and points out how of these concepts differentiates from each other.</p>

<p>Let's first discuss about these concepts and rules to be followed.</p>

### Overriding

<p>Java is an object oriented language. So it is all about classes and objects. We use inheritance when writing Java code, because of it's benefits. It helps to reuse the code and polymorphically refer to objects.</p>

<p>Sub classes can inherit methods from <b>super type</b>. Yes I said super type, because it can be a class or an interface the sub class inherits from. After Java version 8, <b>interfaces can have concrete inheritable methods</b>. These methods are called <b>default methods</b>. Once the sub class inherits the method, it can either keep it as it is or override it if the sub class need to provide it's own specific behaviour to the method.</p>

  

<p>There are some rule need to be followed when overriding a method. <b>Note that same rules apply when providing method implementation for abstract method of interface or abstract class. </b></p>

  

1. Argument list must exactly match that of overridden method
2. Return type must be same or sub type of return type declared in overridden method
3. Access level can not be more restricted than overridden method
4. Access level can be less restrictive than overridden method
5. Overriding method can throw any unchecked exceptions
6. Overriding method can not throw new or wider checked exceptions than the checked exceptions declared in overridden method
7. Overriding method can throw few or narrower checked exceptions than those declared in overridden method
8. Overriding method can eliminate all checked exceptions if those declared in overridden method are unnecessary
9. Method can be overridden only if the method inherited by sub type
10. Can not override **final** or **static** methods

<p>Following is an example of overriding:</p>
<p>Super class:</p>

```java
public class Animal{
public void makeNoice(){
    System.out.println("Generic Animal Noice");
}
}
```
<p>Sub class:</p>

```java
public class Horse extends Animal{
public void makeNoice(){
    System.out.println("Horse Noice");
}
}
```

#### Using @Override
<p>@Override annotation introduced in Java 5 version. This can be used to catch errors when overriding or implementing methods.</p>
<p>Horse sub class after applying @Override annotation:</p>

```java
public class Horse extends Animal{

 @Override   
public void makeNoice(){
    System.out.println("Horse Noice");
}
}
```

### Overloading
<p>Overloading allows to reuse same method name but with different arguments. This helps the caller of the method because the class take care of different argument types without asking the caller to do conversions prior to calling the method. Overloading has less rules than overriding and not that complex</p>

<p>Rules for overloading:</p>

1. Overloaded method **must** change argument list
2. Overloaded method **can** change return type
3. Overloaded method **can** change the access modifier
4. Overloaded method **can** declare new or broader checked exceptions
5. Overloading can be done in same type or sub type

<p>Following is an example of overriding:</p>

```java
public class Monkey{

public void eat(){
    System.out.println("Monkey eats banana");


public void eat(String food){
    System.out.println("Monkey eats " + food);
}

}
```

<p>That's all about overriding and overloading. Now let's summarise the differences between them.</p>

||Overriding| Overloading |
|--|--|--|
|Arguments |Must not change  | Must change |
|Return type |Can not change except sub type of return type declared in overridden method | Can change |
|Access level |Can be less restrictive, but can not be more restrictive  | Can change |
|Checked exceptions |Can not throw new or wider checked exceptions, but can throw less or few checked exceptions than overridden method  | Can throw new or wider checked exceptions than overloading method|
|Unchecked exceptions |Can throw any unchecked exceptions  | Can throw any unchecked exceptions |
|Can be done in |Sub type  | Same type or sub type |
