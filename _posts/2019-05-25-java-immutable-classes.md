---
layout: post
title: "Implement your own immutable class in Java"
date: 2019-05-25 23:21:36 +0800
categories: Java

---

<p>Immutable class's object's instance variable values can not be changed. Immutable classes are thread safe, so they are useful in applications using concurrency/ parallelism. String class, primitive wrapper classes are examples for immutable classes in Java language.</p>

<p>Now let's discuss how can we implement our own immutable classes.</p>

<p>Let's imagine a scenario like this:</p>
<p>We are implementing a photo editing application where user can create his/her own colors by specifying it's RBG values. Following thing need to be allowed in application</p>

1. Create color objects by specifying RGB values
2. Share color objects
3. Users can read the RGB values of color object, but those values can not be changed/ mutated

<p>We can write color class like this:</p>

```java

final  class  Color{

private  final  StringBuilder  colorName;
private  final  int  r;
private  final  int  g;
private  final  int  b;

public  Color(StringBuilder  name, int  red, int  green, int  blue){
this.colorName = new  StringBuilder(name);
this.r = red;
this.g = green;
this.b = blue;
}

// Notice that NO setters available

public  StringBuilder  getColorName(){
return  new  StringBuilder(colorName);
}

public  int  getColor(){
return  this;
}
}

```

<p>Here is a list of steps to consider when implementing an immutable class:</p>

|Step| Description |
|--|--|
|Mark class as final  | Class can not be extended, no room for subclasses and substituting subclass instance for superclass variable |
|Mark instance variables private and final | Instance variable values can not be accessed from other classes, variable values can not be changed |
|No setter methods | Instance variable values can not be changed to different values from other classes|
|If constructor takes mutable objects, create a copy of them and assign to instance variables  | Even mutable object provided to constructor changes instance variable values remain unchanged|
|If getters return mutable object reference, create a copy, return the reference to copy  | Reference returned from getter has no effect on instance variable of immutable object|
