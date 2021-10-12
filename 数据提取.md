# 数据提取

## 1. 正则表达式

### 基本符号

`·`：表示除换行之外所有字符，仅表示单个字符

如："regular" 可以表示为`re...ar`

`*`：表示前一个表达式0次或无限次

`?`：表示前一个表达式0次或1次

`()`：提取括号里的内容

`“.*”`：贪婪模式，获取最长的满足条件的字符串。

`“.*? ”`：非贪婪模式，获取最短的能满足条件的字符串。

### findall()

```
 re.findall(pattern, string, flags=0)
```

以列表形式返回所有满足要求的字符串，如果没有匹配到结果，就会返回空列表

多个“`(.*? )`”返回的仍然是一个列表，但是列表里面的元素变为了元组

```python
re.findall('账号是：(.*?), 密码是：(.*?)', text, re.S)

>>>[('kingname', '123456'), ('shin', '27743')...]
```

“`re.S`”：忽略换行符

### search()

只会返回第1个满足要求的字符串。一旦找到符合要求的内容，它就会停止查找。

匹配成功，则是一个正则表达式的对象；如果没有匹配到任何数据，就是None。

通过.group()这个方法来获取里面的值，且只有在.group()里面的参数为1的时候，才会把正则表达式里面的括号中的结果打印出来。

## 2. XPath

> 为了使用xpath，需要安装lxml XPath返回的是一个列表

`pip install lxml`

### 语法

1. 获取文本:

```python
//标签1[@属性1="属性1"]/标签2[@属性2="属性2"]/.../text()
```

1. 获取属性值：

```python
//标签1[@属性1="属性值1”]/标签2[@属性2="属性2"]/.../@属性n
```

1. XPath特殊情况
   1.  以相同字符串开头

       ```python
       //标签[starts-with(@属性名, "开头相同字符串")]
       ```
   2.  属性值包含相同字符串

       ```python
       //标签[contains(@属性名, "相同字符串")]
       ```
   3.  对Xpath返回的对象执行XPath 例：

       ```python
       useful = html.xpath('//div[@class="useful"]')# 这里返回一个列表
       info_list = useful[0].xpath('ul/li/text()')
       ```
   4.  不同标签下的文字

       ```python
       useful = html.xpath('//div[@id="test1"]')[0]
       info = useful.xpath('string(.)')
       ```

## 3. parsel模块

pass

## 4. Beautiful Soup4

### 安装

`pip install beautifulsoup4`

### 导入

`from bs4 import BeautifulSoup`

### 语法

步骤：

1. 处理源代码生成的BeautifulSoup对象
2. 使用find_all()或者find()来查找内容
   1.  解析源代码

       ```python
       soup = BeautifulSoup(网页源代码, '解析器')# 解析器可以使用lxml
       ```
   2.  查找内容

       ```python
       useful = soup.find(class_='useful')
       all_content = useful.find_all('li')
       for li in all_content：
       print(li.string)
       ```

#### find()与find_all区别

* find_all()返回的是BeautifulSoup Tag对象组成的列表，如果没有找到符合要求的标签则返回空列表
* find()返回的是一个BeautifulSoup Tag对象，如果有多个符合条件的标签，则返回第1个，找不到则返回None

\---------------------------------------------------------=====
