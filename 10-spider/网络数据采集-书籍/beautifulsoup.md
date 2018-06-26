### beautifulSoup



#### 安装包

-   `pip install beautifulsoup4`



#### 导入包

-   `form bs4 import BeautifulSoup`





#### 使用

beautifulSoup得到的是一个 bsObj  我们可以在它的基础上进行获取我们需要的信息

```python


from urllib.request import urlopen
from bs4 import BeautifulSoup

html = urlopen('')
bsObj = BeautifulSoup(html.read())
print(bsObj.h1)  # 获取 h1 标签
```







































