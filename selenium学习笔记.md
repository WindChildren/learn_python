---
title: selenium学习笔记
tags: selenium，python，java
grammar_cjkRuby: true
---


# selenium安装
*  Java


创建maven项目，pom.xml配置如下：
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <groupId>MySel20Proj</groupId>
        <artifactId>MySel20Proj</artifactId>
        <version>1.0</version>
        <dependencies>
            <dependency>
                <groupId>org.seleniumhq.selenium</groupId>
                <artifactId>selenium-server</artifactId>
                <version>3.0.1</version>
            </dependency>
        </dependencies>
</project>
```
* python

```
pip install selenium
```

# webdriver例子

* java

```
package org.openqa.selenium.example;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedCondition;
import org.openqa.selenium.support.ui.WebDriverWait;

public class Selenium2Example  {
    public static void main(String[] args) {
        // Create a new instance of the Firefox driver
        // Notice that the remainder of the code relies on the interface, 
        // not the implementation.
        WebDriver driver = new FirefoxDriver();

        // And now use this to visit Google
        driver.get("http://www.google.com");
        // Alternatively the same thing can be done like this
        // driver.navigate().to("http://www.google.com");

        // Find the text input element by its name
        WebElement element = driver.findElement(By.name("q"));

        // Enter something to search for
        element.sendKeys("Cheese!");

        // Now submit the form. WebDriver will find the form for us from the element
        element.submit();

        // Check the title of the page
        System.out.println("Page title is: " + driver.getTitle());
        
        // Google's search is rendered dynamically with JavaScript.
        // Wait for the page to load, timeout after 10 seconds
        (new WebDriverWait(driver, 10)).until(new ExpectedCondition<Boolean>() {
            public Boolean apply(WebDriver d) {
                return d.getTitle().toLowerCase().startsWith("cheese!");
            }
        });

        // Should see: "cheese! - Google Search"
        System.out.println("Page title is: " + driver.getTitle());
        
        //Close the browser
        driver.quit();
    }
}
```
* python

```
from selenium import webdriver
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.support.ui import WebDriverWait # available since 2.4.0
from selenium.webdriver.support import expected_conditions as EC # available since 2.26.0

# Create a new instance of the Firefox driver
driver = webdriver.Firefox()

# go to the google home page
driver.get("http://www.google.com")

# the page is ajaxy so the title is originally this:
print driver.title

# find the element that's name attribute is q (the google search box)
inputElement = driver.find_element_by_name("q")

# type in the search
inputElement.send_keys("cheese!")

# submit the form (although google automatically searches now without submitting)
inputElement.submit()

try:
    # we have to wait for the page to refresh, the last thing that seems to be updated is the title
    WebDriverWait(driver, 10).until(EC.title_contains("cheese!"))

    # You should see "cheese! - Google Search"
    print driver.title

finally:
    driver.quit()
```

# 查找UI元素

* java

```
WebElement element = driver.findElement(By.id("coolestWidgetEvah"));

List<WebElement> cheeses = driver.findElements(By.className("cheese"));

WebElement frame = driver.findElement(By.tagName("iframe"));

WebElement cheese = driver.findElement(By.name("cheese"));

WebElement cheese = driver.findElement(By.linkText("cheese"));

WebElement cheese = driver.findElement(By.cssSelector("#food span.dairy.aged"));

List<WebElement> inputs = driver.findElements(By.xpath("//input"));
```

* python

```
element = driver.find_element_by_id("coolestWidgetEvah")
or
from selenium.webdriver.common.by import By
element = driver.find_element(by=By.ID, value="coolestWidgetEvah")

cheeses = driver.find_elements_by_class_name("cheese")
or
from selenium.webdriver.common.by import By
cheeses = driver.find_elements(By.CLASS_NAME, "cheese")

frame = driver.find_element_by_tag_name("iframe")
or
from selenium.webdriver.common.by import By
frame = driver.find_element(By.TAG_NAME, "iframe")

cheese = driver.find_element_by_name("cheese")
or
from selenium.webdriver.common.by import By
cheese = driver.find_element(By.NAME, "cheese"

cheese = driver.find_element_by_link_text("cheese")
or
from selenium.webdriver.common.by import By
cheese = driver.find_element(By.LINK_TEXT, "cheese")

cheese = driver.find_element_by_css_selector("#food span.dairy.aged")
or
from selenium.webdriver.common.by import By
cheese = driver.find_element(By.CSS_SELECTOR, "#food span.dairy.aged")

inputs = driver.find_elements_by_xpath("//input")
or
from selenium.webdriver.common.by import By
inputs = driver.find_elements(By.XPATH, "//input")
```

* 执行js查找元素
	* java
`WebElement element = (WebElement) ((JavascriptExecutor)driver).executeScript("return $('.cheese')[0]");`

查找页面上每个标签的所有输入元素
```
List<WebElement> labels = driver.findElements(By.tagName("label"));
List<WebElement> inputs = (List<WebElement>) ((JavascriptExecutor)driver).executeScript(
    "var labels = arguments[0], inputs = []; for (var i=0; i < labels.length; i++){" +
    "inputs.push(document.getElementById(labels[i].getAttribute('for'))); } return inputs;", labels);
```
	* python 
`element = driver.execute_script("return $('.cheese')[0]")`

查找页面上每个标签的所有输入元素
```
labels = driver.find_elements_by_tag_name("label")
inputs = driver.execute_script(
    "var labels = arguments[0], inputs = []; for (var i=0; i < labels.length; i++){" +
    "inputs.push(document.getElementById(labels[i].getAttribute('for'))); } return inputs;", labels)
```
















