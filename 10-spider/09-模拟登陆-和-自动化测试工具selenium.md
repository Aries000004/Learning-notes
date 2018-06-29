



#### 关于selenium 自动化测试框架

​	Selenium是一个开源的和便携式的自动化软件测试工具，用于测试Web应用程序有能力在不同的浏览器和操作系统运行。Selenium真的不是一个单一的工具，而是一套工具，帮助测试者更有效地基于Web的应用程序的自动化。

​	通过 selenium 自动化测试框架可以很好的放置反爬虫的行为， 因为都是在浏览器页面上的操作，筒过selenium 获取页面的信息可以避免 页面时 Ajax 加载数据导致爬虫无法获取数据。



### 使用

-   安装 `pip install selenium`
-   我们通过Selenium实现对Chrome浏览器的操控，如果要操控其他的浏览器，可以创对应的浏览器对象，例如Chrome、Firefox、Edge等，还有手机端的浏览器Android、BlackBerry等，另外无界面浏览器PhantomJS也同样支持。

```python

from selenium import webdriver

# 驱动位置
chromeDriver = 'D:/00venv/soft/chromedriver_win32/chromedriver.exe'
# 初始化 浏览器对象
browser = webdriver.Firefox(Driver)
browser = webdriver.Ie(Driver)
browser = webdriver.Opera(Driver)
browser = webdriver.Chrome(Driver)
browser = webdriver.PhantomJS(Driver)

```

#### 访问 url

`browser.get(url)`



#### 获取元素

注意  element（单个） 和 elements(多个)

`find_element() ` 需要传入两个参数， 一个时查找的方式 by 另一个就是值，实际上它就是`find_element_by_id()`这种方法的通用函数版本。

```python

find_element_by_id()  # 等价于
find_element(By.ID, id)

find_element_by_css_selector('.foo')
find_elements(By.CSS_SELECTOR, '.foo li')
```

>   注意： from selenium.webdriver.common.by import By



```python

find_element_by_name()  #根据 name 值来获取
find_element_by_id()  # id 获取
find_element_by_xpath()  # xpath
find_element_by_css_selector('.foo') # 更具 CSS 的选择器来获取 

```



#### 延时等待

-   在Selenium中，get()方法会在网页框架加载结束之后就结束执行，此时如果获取page_source可能并不是浏览器完全加载完成的页面，如果某些页面有额外的Ajax请求，我们在网页源代码中也不一定能成功获取到。所以这里我们需要延时等待一定时间确保元素已经加载出来。在这里等待的方式有两种，一种隐式等待，一种显式等待。

隐式等待

-   `browser.implicitly_wait(4)`

>   selenium.webdriver.remote.webdriver.implicitly_wait(time_to_wait)
>
>   隐式地等待一个无素被发现或一个命令完成；这个方法每次会话只需要调用一次

显示等待

-   `time.sleep()`



#### 前进后退

-   `browser.back()`
-   `browser.forward()`



#### 切换窗口

```python

import time

from selenium import webdriver


chromeDriver = 'D:/00venv/soft/chromedriver_win32/chromedriver.exe'

browser = webdriver.Chrome(chromeDriver)

# 打开浏览器， 访问 淘宝
browser.get('http://www.taobao.com/')

# 首页窗口 处理手柄
tabao_hander = browser.current_window_handle

# 等待5 秒
browser.implicitly_wait(5)

# 进行 Xpath 获取元素 并且执行点击事件
# a = browser.find_element_by_xpath('/html/body/div[4]/div[1]/div[1]/div[1]/div/ul/li[1]/a[1]')
# a.click()

# 女装窗口 处理手柄
# nvzhuang_hander = browser.current_window_handle

# 休眠 3 秒
# time.sleep(3)

# 切换窗口 到首页
# browser.switch_to_window(tabao_hander)

# 输入搜索内容并进行搜索
browser.find_element_by_id('q').send_keys('笔记本电脑')

# 点击搜索按钮
browser.find_element_by_xpath('//*[@id="J_TSearchForm"]/div[1]/button').click()

time.sleep(3)
# 回退
# browser.back()
#
# time.sleep(3)
# # 前进
# browser.forward()

# 执行 JS  页面向下滚动
browser.execute_script('document.documentElement.scrollTop=2000')

# 到顶部
browser.execute_script('window.scrollTo=(0,0)')

# 只会关闭当前窗口
# browser.close()
time.sleep(5)
# 关闭浏览器
browser.quit()
```



#### Cookies操作

```python

from selenium import webdriver

chromedriver = 'C:\Program Files (x86)\Google\Chrome\Application\chromedriver'
browser = webdriver.Chrome(chromedriver)
browser.get('https://www.zhihu.com/explore')

# 获取所有的 cookies 信息
browser.get_cookies()

# 添加一个 cookie 信息
browser.add_cookie()

# 删除所有的 cookies
browser.delete_all_cookies()

browser.close()
```





#### [Python-requests.Session模拟登陆](https://www.cnblogs.com/whatbeg/p/5320666.html)