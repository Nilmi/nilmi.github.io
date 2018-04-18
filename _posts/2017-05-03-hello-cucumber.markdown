---
layout: post
title:  "Create a Cucumber test with Selenium and Java"
date:   2017-02-05 10:20:24 +0530
categories: Cucumber
---
<p>There are three different components you need to think about when creating automated test cases using Cucumber, Selenium and Java. </p>

- Feature file - contains Gherkin sentences with Cucumber keywords
- Step definition file - contains Selenium, Java code with annotations to map feature file with step definition file
- Test runner - to run the feature file and generate reports

<p>Let's say we need to automate following scenario,</p>
**Scenario:** Navigate to test url (home page), enter username and password and click on login button <br />
**We need to verify:** Title of the home page and title of after login
