---
layout: post
title:  "Selenium Waits"
date:   2017-04-12 16:40:15 +0530
categories: Selenium WebDriver
---
![image-title-here](/images/selenium/implicit-and-explicit-wait/wait.png){:class="img-responsive"}

There are different kinds of waits in Selenium. Wait can be used to save your scripts from failing because of network delays, elements not loaded at the time of script execution etc. Instead of using thread.sleep to synchronize your code, you can choose appropriate wait which suites for the situation.
<p>Let’s discuss about wait commands in Selenium and finally about thread.sleep and it’s disadvantages.</p>

### 1. Explicit wait

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

WebDriverWait is a sub class of FluentWait . According to above code you can configure web driver wait object to wait until specified expected condition is true.

### 2.  Implicit wait
When an implicit wait is implemented in tests, if WebDriver cannot find an element in the Document Object Model (DOM), it will wait for a defined amount of time for the element to appear in the DOM. In other terms, an implicit wait polls the DOM for a certain amount of time when trying to find an element or elements if they are not immediately available.
Once set implicit wait is set for lifetime of driver object and for all elements.
#### Disadvantages:
The downside is if you set the waiting limit to be 5 seconds and the elements appears in the DOM in 6 seconds, your tests will fail because you configuration is to wait a maximum of 5 seconds.

{% highlight ruby %}
public static void implicitWait(WebDriver driver) {
 driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
}
{% endhighlight %}

To summarize: Implicit wait time is applied to all elements in your script and Explicit wait time is applied only for a particular specified element.

### 3.  Fluent wait
As I mentioned earlier FluentWait is the super class of WebDriverWait. When we are using the FluentWait instance, we can specify:
..The frequency with which FluentWait has to check the conditions defined.
..Ignore specific types of exception waiting such as NoSuchElementExceptions while searching for an element on the page.
..Maximum amount of time to wait for a condition.

Below is a sample code for fluent wait.
{% highlight ruby %}
Wait wait = new FluentWait(driver) .withTimeout(30, SECONDS) .pollingEvery(5, SECONDS) .ignoring(NoSuchElementException.class);
{% endhighlight %}

An example of fluent wait:
<p>Let’s say you have an element which sometime appears in just 4 second and some time it takes minutes to appear. In that case it is better to use fluent wait, as this will try to find element again and again until it find it or until the final timer runs out.</p>

### 4.  PageLoadTimeout
Sets the amount of time to wait for a page load to complete before throwing an error. If you set the timeout as a negative value, page loads can be indefinite.
{% highlight ruby %}
driver.manage().timeouts().pageLoadTimeout(100, SECONDS);
{% endhighlight %}

### 5. SetScriptTimeout
SetScriptTimeout configures the amount of time to wait for an asynchronous script to finish execution before throwing an error. If the timeout is set to a negative value, script will be allowed to run indefinitely.
{% highlight ruby %}
driver.manage().timeouts().setScriptTimeout(100,SECONDS);
{% endhighlight %}

### Thread sleep
<p>Finally what about thread sleep? Thread sleep forces the browser to wait for a specific time, this is rarely used in Selenium scripts. </p>
<p>Selenium provide   the above mentioned waits which can be matched with the situation you need to handle. So if you specify them in your code you can specify much better timeout values which make the tests more reliable. Since the condition evaluated time to time, those waits not slowing the tests down. So to conclude using thread.sleep is not a good idea, always try to use Selenium waits.</p>



[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
