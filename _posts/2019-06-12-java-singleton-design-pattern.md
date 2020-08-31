---

layout: post
title: "Singleton Design Pattern"
date: 2019-06-12 23:12:20 +0800
categories: Java

---

<p>This article describes details about singleton design pattern and how to implement singleton design pattern in Java.</p>
<p>We can use singleton design pattern to make sure there is only one instance of a class within the application. Singleton is called creational design pattern because it is related to creating objects.</p>
<p>Key things to be considered when implementing singleton class are:</p>

1. Private static variable to store the single instance - usually this is final (prevent accidentally changing the value)
2. Public static method to get reference to the instance
3. Private constructor - Other classes can not create instances directly by calling the constructor

<p>There are two different approaches we can take to initialize the single instance.</p>

<p>To discuss the implementation of singleton design pattern, let's assume we need to implement an online game which has a score board. When players record new high score, the score should update in the score board. There should be one score board within the application.</p>

### 1. Eager Initialization

<p>Creates the single object before the first use of the class. Following is an example of singleton patten implementation using eager initialization:</p>

```java
public  class  ScoreBoard{

private  static  final  ScoreBoard  INSTANCE = new  ScoreBoard();

private  ScoreBoard(){
// ScoreBoard constructor code goes here
}

public  static  ScoreBoard  getInstance(){
return INSTANCE;
}
}
```

### 2. Lazy Initialization
<p>Creates the single object after the first use of the class. Following is an example of singleton patten implementation using lazy initialization:</p>

```java
public  class  ScoreBoard{

private  static  ScoreBoard  INSTANCE;

private  ScoreBoard(){
// ScoreBoard constructor code goes here
}

public  static  ScoreBoard  getInstance(){
	if(INSTANCE == null){
	INSTANCE = new  ScoreBoard();
	}
return INSTANCE;
}
}
```

### Make Singleton Class Thread Safe
<p> Above singleton implementation assumes we are running only one thread at a time. So it is not thread safe. To make the singleton implementation thread safe we can use **synchronized** keyword to getInstance method.</p>

  
### Benefits of Singleton Design Pattern
1. Maintain only one instance of a class
2. Some objects are expensive to create. By maintaining single instance of such objects helps to improve performance of application.