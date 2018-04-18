---
layout: post
title:  "How to handle frames?"
date:   2018-01-05 08:10:20 +0530
categories: Selenium WebDriver
---
<p>Sometimes you do all the coding right but still when you run your code it gives you NoSuchElementException. Here is another possible reason for that...</p>

<p>According to the hierarchy of WebElements usually WebElements are located on web page. But there are some cases WebElements are located on frames which are located on web page. So is there a way to check whether this bugging WebElement located on a frame? Luckily Yes :) </p>

<p>On your browser, right click on just after the WebElement. Check whether option  "View Frame Source" (Chrome Browser)/ "This Frame" (FireFox browser) available. If it's yes, then the WebElement located on a frame.</p>

![image-title-here](/images/selenium/how-to-handle-frames/chrome.png){:height="200px" width="200px"}

To access elements in frames first we need to switch the driver from browser web page to frame. These are the steps,
1. Inspect the frame and identify a locator to locate frames
2. Use driver.switchTo().frame(name_or_id) to switch the driver to frames
3. Then write the code as usually

Let's say we need to automate following set of activities.
1. Go to the url
2. Enter username and password and login
3. Click on certain button (which is located on a frame)

<p>So how the code looks like? and the biggest question how to switch the driver to the frame? Let's see...</p>

Code looks like this,

{% highlight ruby %}
// set chrome driver property and launch Chrome
System.setProperty("webdriver.chrome.driver","your ChromeDriver path");
WebDriver driver  = new ChromeDriver();

// Set variables
String baseUrl = "your url";

//navigate to web page
driver.get(baseUrl);

//enter username and password and login
driver.findElement(By.id("username")).sendKeys("Your username");
driver.findElement(By.id("password")).sendKeys("Your password");
driver.findElement(By.id("submit")).click();

//switch to frame
driver.switchTo().frame("frame name");

//click on link
Driver.findElement(By.name("link name")).click();
{% endhighlight %}

As you already guessed **driver.switchTo().frame("frame name");** this line of code changes the driver focus to frame.
