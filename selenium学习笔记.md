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

# webdriver
## 例子
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

## 查找UI元素

* java

```
WebElement element = driver.findElement(By.id("coolestWidgetEvah"));
//获取文本内容
element.getText();

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
#获取文本内容
element.text()

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

 java
`WebElement element = (WebElement) ((JavascriptExecutor)driver).executeScript("return $('.cheese')[0]");`
查找页面上每个标签的所有输入元素
```
List<WebElement> labels = driver.findElements(By.tagName("label"));
List<WebElement> inputs = (List<WebElement>) ((JavascriptExecutor)driver).executeScript(
    "var labels = arguments[0], inputs = []; for (var i=0; i < labels.length; i++){" +
    "inputs.push(document.getElementById(labels[i].getAttribute('for'))); } return inputs;", labels);
``` 

python
`element = driver.execute_script("return $('.cheese')[0]")`
查找页面上每个标签的所有输入元素
```
labels = driver.find_elements_by_tag_name("label")
inputs = driver.execute_script(
    "var labels = arguments[0], inputs = []; for (var i=0; i < labels.length; i++){" +
    "inputs.push(document.getElementById(labels[i].getAttribute('for'))); } return inputs;", labels)
```

* 点击方法

 java
 
`driver.findElement(By.id("submit")).click();`

 python
 
`driver.find_element_by_id("submit").click()`

* 弹窗切换跳转

java

`driver.switchTo().window("windowName");`

python

`driver.switch_to.window("windowName")`

也可以利用switch进行窗口和弹框切换，改为“frame”或“alert”即可。

在Java中：
`driver.navigate().to("http://www.example.com");`
与
`driver.get("http://www.example.com")`
等效，在python中没有这个方法

## Cookies使用

* java

```
// Go to the correct domain
driver.get("http://www.example.com");

// Now set the cookie. This one's valid for the entire domain
Cookie cookie = new Cookie("key", "value");
driver.manage().addCookie(cookie);

// And now output all the available cookies for the current URL
Set<Cookie> allCookies = driver.manage().getCookies();
for (Cookie loadedCookie : allCookies) {
    System.out.println(String.format("%s -> %s", loadedCookie.getName(), loadedCookie.getValue()));
}

// You can delete cookies in 3 ways
// By name
driver.manage().deleteCookieNamed("CookieName");
// By Cookie
driver.manage().deleteCookie(loadedCookie);
// Or all of them
driver.manage().deleteAllCookies();
```

* python

```
# Go to the correct domain
driver.get("http://www.example.com")

# Now set the cookie. Here's one for the entire domain
# the cookie name here is 'key' and its value is 'value'
driver.add_cookie({'name':'key', 'value':'value', 'path':'/'})
# additional keys that can be passed in are:
# 'domain' -> String,
# 'secure' -> Boolean,
# 'expiry' -> Milliseconds since the Epoch it should expire.

# And now output all the available cookies for the current URL
for cookie in driver.get_cookies():
    print "%s -> %s" % (cookie['name'], cookie['value'])

# You can delete cookies in 2 ways
# By name
driver.delete_cookie("CookieName")
# Or all of them
driver.delete_all_cookies()
```
## 拖放事件

* java

```
WebElement element = driver.findElement(By.name("source"));
WebElement target = driver.findElement(By.name("target"));

(new Actions(driver)).dragAndDrop(element, target).perform();
```

* python

```
from selenium.webdriver.common.action_chains import ActionChains
element = driver.find_element_by_name("source")
target =  driver.find_element_by_name("target")

ActionChains(driver).drag_and_drop(element, target).perform()
```

# WebDriver’s Drivers
## HtmlUnit Driver
This is currently the fastest and most lightweight implementation of WebDriver. As the name suggests, this is based on HtmlUnit. HtmlUnit is a java based implementation of a WebBrowser without a GUI. For any language binding (other than java) the Selenium Server is required to use this driver.
* java

`WebDriver driver = new HtmlUnitDriver();`

* python

`driver = webdriver.Remote("http://localhost:4444/wd/hub", webdriver.DesiredCapabilities.HTMLUNIT.copy())`

## Firefox Driver
* java

`WebDriver driver = new FirefoxDriver();`
一般默认会去找默认安装的C盘位置，如果不在，则自己指定告诉火狐浏览器位置
`System.setProperty("webdriver.firefox.bin","D:\\Firefox\\firefox.exe");`

设置配置文件
```
// 设置是否询问下载位置（可忽略）；默认true——不询问，直接下载到指定路径，具体设置见browser.folderList，false——询问
profile.setPreference("browser.download.useDownloadDir",true);
// 指定下载位置
profile.setPreference("browser.download.downloadDir", "c:\\OutputFolder");
// 设置下载方式；0——下载到桌面，默认1——下载到Firefox默认位置，2——下载到指定位置
profile.setPreference("browser.download.folderList", 2);
// 当一个下载开始时，设置是否显示下载管理器；默认true——显示，flase——不显示
profile.setPreference("browser.download.manager.showWhenStarting",false);
```

* python 

`driver = webdriver.Firefox()`

# 隐式和显式等待

在继续下一步之前，等待使自动化任务执行经过一定时间。您应该选择使用显式等待或隐式等待。

## 显式等待

* java

```
WebDriver driver = new FirefoxDriver();
driver.get("http://somedomain/url_that_delays_loading");
WebElement myDynamicElement = (new WebDriverWait(driver, 10))
  .until(ExpectedConditions.presenceOfElementLocated(By.id("myDynamicElement")));
```

* python
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait # available since 2.4.0
from selenium.webdriver.support import expected_conditions as EC # available since 2.26.0

ff = webdriver.Firefox()
ff.get("http://somedomain/url_that_delays_loading")
try:
    element = WebDriverWait(ff, 10).until(EC.presence_of_element_located((By.ID, "myDynamicElement")))
finally:
    ff.quit()
```

## 隐式等待
* java

```WebDriver driver = new FirefoxDriver();
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
driver.get("http://somedomain/url_that_delays_loading");
WebElement myDynamicElement = driver.findElement(By.id("myDynamicElement"));
```

* python

```from selenium import webdriver

ff = webdriver.Firefox()
ff.implicitly_wait(10) # seconds
ff.get("http://somedomain/url_that_delays_loading")
myDynamicElement = ff.find_element_by_id("myDynamicElement")
```

# 截取屏幕截图

* java

```
import java.io.File;
import java.net.URL;

import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.remote.Augmenter;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;

public class Testing {
    
    public void myTest() throws Exception {
        WebDriver driver = new RemoteWebDriver(
                                new URL("http://localhost:4444/wd/hub"), 
                                DesiredCapabilities.firefox());
        
        driver.get("http://www.google.com");
        
        // RemoteWebDriver does not implement the TakesScreenshot class
        // if the driver does have the Capabilities to take a screenshot
        // then Augmenter will add the TakesScreenshot methods to the instance
        WebDriver augmentedDriver = new Augmenter().augment(driver);
        File screenshot = ((TakesScreenshot)augmentedDriver).
                            getScreenshotAs(OutputType.FILE);
    }
}
```

* python

```
from selenium import webdriver

driver = webdriver.Remote("http://localhost:4444/wd/hub", webdriver.DesiredCapabilities.FIREFOX.copy())
driver.get("http://www.google.com")
driver.get_screenshot_as_file('/Screenshots/google.png')
```

# 浏览器启动操作

## 使用代理
### IE浏览器

* java

```
String PROXY = "localhost:8080";

org.openqa.selenium.Proxy proxy = new org.openqa.selenium.Proxy();
proxy.setHttpProxy(PROXY)
     .setFtpProxy(PROXY)
     .setSslProxy(PROXY);
DesiredCapabilities cap = new DesiredCapabilities();
cap.setCapability(CapabilityType.PROXY, proxy);

WebDriver driver = new InternetExplorerDriver(cap);
```
* python

```
from selenium import webdriver

PROXY = "localhost:8080"

# Create a copy of desired capabilities object.
desired_capabilities = webdriver.DesiredCapabilities.INTERNETEXPLORER.copy()
# Change the proxy properties of that copy.
desired_capabilities['proxy'] = {
    "httpProxy":PROXY,
    "ftpProxy":PROXY,
    "sslProxy":PROXY,
    "noProxy":None,
    "proxyType":"MANUAL",
    "class":"org.openqa.selenium.Proxy",
    "autodetect":False
}

# you have to use remote, otherwise you'll have to code it yourself in python to 
# dynamically changing the system proxy preferences
driver = webdriver.Remote("http://localhost:4444/wd/hub", desired_capabilities)
```

### chorme
使用方法基本与IE浏览器相同

### Firefox up to version 47.0.1

* java

```
String PROXY = "localhost:8080";

org.openqa.selenium.Proxy proxy = new org.openqa.selenium.Proxy();
proxy.setHttpProxy(PROXY)
     .setFtpProxy(PROXY)
     .setSslProxy(PROXY);
DesiredCapabilities cap = new DesiredCapabilities();
cap.setCapability(CapabilityType.PROXY, proxy);
WebDriver driver = new FirefoxDriver(cap);
```
Firefox version 48 and newer - GeckoDriver
```
String PROXY = "localhost";
int PORT = 8080;

com.google.gson.JsonObject json = new com.google.gson.JsonObject();
json.addProperty("proxyType", "MANUAL");
json.addProperty("httpProxy", PROXY);
json.addProperty("httpProxyPort", PORT);
json.addProperty("sslProxy", PROXY);
json.addProperty("sslProxyPort", PORT);

DesiredCapabilities cap = new DesiredCapabilities();
cap.setCapability("proxy", json);

GeckoDriverService service =new GeckoDriverService.Builder(firefoxBinary)
  .usingDriverExecutable(new File("path to geckodriver"))
  .usingAnyFreePort()
  .usingAnyFreePort()
  .build();
service.start();

// GeckoDriver currently needs the Proxy set in RequiredCapabilities
driver = new FirefoxDriver(service, cap, cap);
```
* python 

```
from selenium import webdriver
from selenium.webdriver.common.proxy import *

myProxy = "host:8080"

proxy = Proxy({
    'proxyType': ProxyType.MANUAL,
    'httpProxy': myProxy,
    'ftpProxy': myProxy,
    'sslProxy': myProxy,
    'noProxy': '' # set this value as desired
    })

driver = webdriver.Firefox(proxy=proxy)

# for remote
caps = webdriver.DesiredCapabilities.FIREFOX.copy()
proxy.add_to_capabilities(caps)

driver = webdriver.Remote(desired_capabilities=caps)
```









