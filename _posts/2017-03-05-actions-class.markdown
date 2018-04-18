---
layout: post
title:  "Actions Class"
date:   2017-03-05 10:48:15 +0530
categories: Selenium WebDriver
---
<p>Actions class can be used to handle different keyboard and mouse events. Actions class is available in org.openqa.selenium.interactions package.</p>

<p>Following are some of the actions which can be performed using actions class.</p>
- Drag and drop
- Perform mouse hover
- Perform mouse hover and click

### Drag and drop elements using Actions class
<p>In following code I have created a method to drag "source" web element to "target" web element. So that we can pass two web elements and driver instance to drag the source web element to target web element.</p>

{% highlight ruby %}
public static void dragAndDrop(WebDriver driver, WebElement source, WebElement target) {
	Actions action = new Actions(driver);
	// to perform drag and drop action in UI need to call perform method
	action.dragAndDrop(source, target).perform();
}
{% endhighlight %}

### Hover / Hover and click using Actions class
<p>Let's check following example:</p>
<p> I have created two methods.</p>

- hover method
- hoverAndClick method

<p>Hover method can be used to hover an element. First of all you need to create an object of actions class. moveToElement() of actions class moves mouse to middle of the element. Use perform() perform action in UI.</p>

{% highlight ruby %}
public static void hover(WebDriver driver, WebElement hoverElement) {
	Actions action = new Actions(driver);
	action.moveToElement(hoverElement).perform();
}
{% endhighlight %}

<p>Consider a scenario like this, first you click on a menu item and then another menu appears and you click on a menu item from that menu. HoverAndClick method can be used for that kind of scenario.</p>
<p> First of all you need to create an object of actions class. Call  moveToElement() which moves mouse to the next element and click() clicks on next element. But can not directly call perform() because there are 2 composite operations therefore call build(). Build generates composite action with all the actions so far ready to perform -> then call perform() </p>

{% highlight ruby %}
public static void hoverAndClick(WebDriver driver, WebElement elementToHover,WebElement elementToClick ) {
	Actions action = new Actions(driver);
	action.moveToElement(elementToHover).click(elementToClick).build().perform();
}
{% endhighlight %}

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
