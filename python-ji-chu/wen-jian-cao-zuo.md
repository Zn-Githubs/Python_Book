# 文件操作

## 文件操作

### 读/写文本文件

#### open

> 需要手动关闭

```python
 f = open(’文件路径’, ’文件操作方式’,encoding='utf-8')
 对文件进行操作
 f.close()
```

#### with open

> 不需要手动关闭，只要代码退出了缩进，Python就会自动关闭文件

```python
 with open(’文件路径’, ’文件操作方式’, encoding='utf-8') as f:
     对文件进行操作
```

### 读文本文件

```python
 with open('text.txt', 'r',encoding='utf-8') as f:
 通过f来读文件
```

在读文件的时候，“文件操作方式”这个参数可以省略，也可以写成“r”，也就是read的首字母。

参数“encoding”可以在打开文件的时候将文件转换为UTF-8编码格式，从而避免乱码的出现，如果文件是在Windows中创建的，并且使用UTF-8打开文件出现了乱码，可以把编码格式改为GBK。

`f.readlines()`：读取所有行，并以列表的形式返回结果，有换行符的话每行后面会带有'/n'

`f.read()`：直接把文件里面的全部内容用一个字符串返回

### 写文本文件

```python
 with open('new.txt', 'w', encoding='utf-8') as f:
     通过f来写文件
```

参数“w”是英文write的首字母，意思是以写的方式打开文件。

这个参数为“w”时为覆盖添加，“a”为附加将新内容写到原文件的末尾

`f.write("一大段文字")`：直接将一大段字符串写入到文本中

`writelines([’第一段话’, ’第二段话’, ’第三段话’])`：将列表里面的所有字符串写入到文本中，如果需要换行则要在‘话’后面添加'/n'

### 读/写CSV文件

### 读CSV文件

首先需要导入CSV模块

```python
 import csv
 with open('文件名.csv', encoding='utf-8') as f:
     reader = csv.DictReader(f)
     for row in reader:
         username = row['username']
         content = row['content']
         reply_time = row['reply_time']
```

for循环得到的row是OrderedDict（有序字典），可以直接像普通字典那样使用：

### 写CSV文件

需要用到`csv.DictWriter()`这个类。它接收两个参数：

第1个参数是文件对象 f；

第2个参数名为 fieldnames，值为字典的Key列表。

`writer.writeheader()`：写入CSV文件的列名行

`writer.writerows(包含字典的列表)`：将包含字典的列表全部写入到CSV文件中

`writer.writerow(字典)`：写入单个字典

```python
 data = [{'name' : 'kingname', 'age' = 24, 'salary' = 9999},
 {'name' : 'meiji ', 'age' = 18, 'salary' = 23},
 {'name' : '小明', 'age' = 27, 'salary' = 45}]
 with open('new.csv', 'w', encoding='utf-8') as f:
     writer = csv.DictWriter(f, fieldnames=['name', 'age', 'salary']
     writer.writeheader()
     writer.writerows(data)
     writer.writerow({'name' : '超人', 'age' : 999, 'salary' : 0})
```
