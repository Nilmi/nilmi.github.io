---
layout: post
title:  "Implicit and Explicit Wait"
date:   2017-04-12 16:40:15 +0530
categories: Selenium WebDriver
---
![image-title-here](/images/selenium/implicit-and-explicit-wait/wait.png){:class="img-responsive"}

Two types of waits in Selenium.

## 1. Explicit wait

This will make your code to wait for certain expected condition to occur before moving forward.
An explicit wait can be used where synchronization is needed, for example, the page is loaded but we are still waiting for a call to complete and an element to appear.
Selenium WebDriver provides,
..WebDriverWait
..ExpectedCondition
classes for implementing an explicit wait. The ExpectedCondition class provides a set of predefined conditions to wait before proceeding further in the code. An example of an explicit wait is:

{% highlight ruby %}
WebDriverWait wait = new WebDriverWait(driver, 10);
wait.until(ExpectedConditions.titleContains("selenium"));  //ExpectedConditions.elementTo BeVisible()/clickable()
{% endhighlight %}

Or

{% highlight ruby %}
	public static void explicitWait(WebDriver driver, String text) {
(new WebDriverWait(driver, 10)).until(ExpectedConditions.elementToBeClickable(By.partialLinkText(text)));
	}
{% endhighlight %}

New object of WebDriverWait -> call until method which is inherited from FluentWait class -> wait until expected conditions is true

## 2.  Implicit wait
When an implicit wait is implemented in tests, if WebDriver cannot find an element in the Document Object Model (DOM), it will wait for a defined amount of time for the element to appear in the DOM. In other terms, an implicit wait polls the DOM for a certain amount of time when trying to find an element or elements if they are not immediately available.
Once set implicit wait is set for lifetime of driver object and for all elements.
### Disadvantages:
Implicit waits can slow down your tests, because once set, the implicit wait is set for the life of the WebDriver object’s instance. This means that when an application responds normally, it will still wait for each element to appear in the DOM which increases the overall execution time.
Another downside is if for example you set the waiting limit to be 5 seconds and the elements appears in the DOM in 6 seconds, your tests will fail because you told it to wait a maximum of 5 seconds.

{% highlight ruby %}
	public static void implicitWait(WebDriver driver) {
		driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	}
  {% endhighlight %}

WebDriver class -> method manage() -> returns Interface WebDriver.Options -> call timeout method of options ->  returns Interface WebDriver.Timeouts -> call implicitlyWait()

To summarize: Implicit wait time is applied to all elements in your script and Explicit wait time is applied only for a particular specified element.


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
