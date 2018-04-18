---
layout: post
title:  "Handle Popup Windows"
date:   2017-03-11 10:50:05 +0530
categories: Selenium WebDriver
---
<p>Let's say we need to automate following set of actions:</p>
- Navigate to the url
- click on a specific link, this will open a popup window
- close the popup window

<p>So how can we close popup windows using Selenium WebDriver? Let's discuss today.</p>

<p>Following is a sample code to do those set of actions, but still this code doesn't work. Mmm.. what is missing here?</p>

{% highlight ruby %}
// set chrome driver property
System.setProperty("webdriver.chrome.driver","your ChromeDriver path");
WebDriver driver  = new ChromeDriver();

// Set variables
String baseUrl = "url";

//navigate to web page
driver.navigate().to(baseUrl);

//click on popup link
driver.findElement(By.linkText("HtmlPopup ")).click();

//close the popup
driver.findElement(By.id("Close")).click();
}
{% endhighlight %}

<p>As the second step you click on that specific link, this opens a popup window, but WebDriver doesn't know that there is a new popup. So even though you write the code to close the popup (click on close button on popup) it still trying to find WebElement on main page. So we need to focus browser to popup window. </p>

<p>Now Let's modify the code.</p>

{% highlight ruby %}
// set chrome driver property
System.setProperty("webdriver.chrome.driver","your ChromeDriver path");
WebDriver driver  = new ChromeDriver();

// Set variables
String baseUrl = "url";

//navigate to web page
driver.navigate().to(baseUrl);

//click on popup link
driver.findElement(By.linkText("HtmlPopup ")).click();

//switch to popup window
		for(String windowName : driver.getWindowHandles()) {
			driver.switchTo().window(windowName);
		}

//close the popup
driver.findElement(By.id("Close")).click();
}
{% endhighlight %}

<p>Note that,</p>
1. I have added getWindowHandles method to get set of windows and their handle.
This will get no of open windows for that browser
2. Iterate through getWindowHandles() results using a for and switch to popup window.
3. Then passed the handle to winodow() of the webDriver instance variable.

<p>Using these steps I have switched to driver the popup window. Then remaining code (close the popup window) will work as expected. </p>
