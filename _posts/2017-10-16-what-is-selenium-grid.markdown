---
layout: post
title:  "What is Selenium Grid?"
date:   2017-10-16 11:10:30 +0530
categories: Selenium Grid
---

<p>Selenium Grid allows to run tests on different machines against different browsers in parallel. That is running multiple tests at the same time against different machines,  different browsers and operating systems.
Essentially, Selenium grid support distributed test execution.
</p>
<p> Selenium Grid has Hub and Node architecture.</p>

### Hub
<p>The Hub The hub is the central point where we load our tests into. There should only be one hub in a grid. The hub is launched only on a single machine, for example a computer whose operating system is Windows 10 and whose browser is IE. </p>

### Nodes
<p>Nodes are the Selenium instances that will execute the tests that we on the hub. There can be one or more nodes in a grid. Nodes can be launched on multiple machines with different platforms and browsers. The machines running the nodes need not be the same platform as that of the hub.</p>

![Selenium Grid](/images/selenium-grid/what-is-selenium-grid/selenium-grid.png){:class="img-responsive"}

<p>Nodes need to register with the Selenium Server. After that if you try to execute a test, this request goes to the server and server knows which node can execute this test (which node having matching utilities for the test, for example: matching browser, operating system).
</p>

### Now let's check the configuration of hub and node.

#### Configuring Hub:
**Step 1**
<p>Go to the machine which you need to setup as hub and download the Selenium Server jar file.</p>

**Step 2**
<p>Place the Selenium Server .jar file anywhere in your HardDrive.</p>

**Step 3**
<p>Go to the directory where you placed the Selenium Server .jar file from the command prompt. Type</p>
{% highlight ruby %}
java -jar selenium-server-standalone-2.30.0.jar -role hub
{% endhighlight %}
<p>The hub should successfully be launched.</p>

#### Configuring Node:
**Step 1**
<p>Go to Machine you need to setup as node and download the Selenium Server jar file.</p>

**Step 2**
<p>Place the Selenium server .jar file anywhere in the drive. Launch a command prompt and navigate to driver location where the Selenium server .jar file is available. Type the code below. IP address and port '10.101.16.255' used here the that is where the hub is running. We also used port 5557 though you can choose any free port number you desire.</p>
{% highlight ruby %}
Java -jar selenium-server-standalone-2.46.0.jar -role webdriver -hub http:10.101.16.255.4444/grid/register -port 5557
{% endhighlight %}

### Set desired capabilities in code
<p>Then we need to set desired capabilities in code required for RemoteWebDriver.
Note: For this code we need to use RemoteWebDriver not the WebDriver.

Desired capabilities are used to set some properties for WebDriver, since not all server implementation will every webDriver feature supports.
Desired capabilities need to set in Selenium Grid setup for webDriver client code are,
Platform
BrowserName

Note: You can check browser and platform details of nodes from hub’s grid console. Just open the url displayed in cmd in browser. (localhost:port or 4444/grid/console)
