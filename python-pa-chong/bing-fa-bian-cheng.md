# 并发编程

## 并发编程

### 程序、进程、线程的基本概念

* 程序：由源代码组成的可执行文件
* 进程：程序运行资源（内存资源）分配的最小单位；一个进程下可以有多个线程，但是至少有一个线程（主线程）；进程之间相互独立，互不影响，资源也不共享
* 线程：CPU调度的最小单位，必须依赖

### 创建多线程的两种方式

```python
 # 直接创建不使用多线程
 import time
 
 def download():
     print('开始下载')
     time.sleep(2)
     print('下载结束')
     
 if __name__ == '__main__':
     download()
```

#### 方法一

> target：指定的是需要执行多线程任务的函数名
>
> args：可以传递元组形式的参数给执行的函数

```python
 # 直接创建多线程
 # 步骤：
 # 1.创建线程
 # 2.启动线程
 
 import time, threading
 
 def download(filename):
     print(filename'开始下载')
     time.sleep(2)
     print(filename'下载结束')
     
 if __name__ == '__main__':
     # 使用循环创建3个线程
     for i in rang(3)：
         # 创建线程
         t = threading.Tread(target=download, args=(i,))
         # 启动线程
         t.start()
```

#### 方法二

```python
 # 使用类创建多线程（推荐）
 # 步骤：
 # 1.自定义一个类并继承Tread类
 # 2.覆写run()方法
 
 import time, threading
 
 class MyThread(threading.Tread):
     # 如果需要传参则需要定义初始化方法
     def __init__(self, filename):
         # 处理父类的init
         #   方法一：
         # threading.Tread.__init__(self)
         #   方法二：
         super().__init__()# super()就相当于threading.Tread
         self.filename = filename
     
     # 覆写run方法
     def run(self):
         print(self.filename, '开始下载')
         time.sleep(2)
         print(self.filename, '下载结束')
         
 if __name__ == '__main__':
     # 使用循环创建3个线程
     for i in rang(3)：
         # 实例化对象（创建线程）
         t = MyTread(i)# 传参需要定义初始化方法并处理父类的init
         # 启动线程，会自动执行run()方法
         t.start()
```

### 线程名称

> 主要应用于调错

```python
 import threading
 
 class MyTread(threading.Tread):
     def run(self):
         # treading.current_thread：查看当前运行的线程
         # 输出结果为：<MyTread(Tread-1, started 4408)
         print('{}正在运行'.format(threading.current_thread()))
         # name属性查看线程的名称，默认为Tread-n
         print('{}正在运行'.format(self.name))
         
 if __name__ == '__main__':
     # 可以在实例化对象是传入name属性，修改线程名称
     t = MyTread(name = 'file{}'.format('新名称'))
     t.start()
```

### 互斥锁

> 线程之间共享全局变量的安全性问题

```python
 import threading
 
 # 创建锁
 lock = threading.Lock()
 # 定义初始值，0为数值型，不可变类型
 value = 0
 # 定义加1函数
 def add_value():
     # 在函数中对全局变量中的不可变类型进行修改需要先global
     global value
     # 加锁（哪里有问题在哪里加锁）
     lock.acquire()
     for i in range(100000):
         value += 1
     # 释放锁
     lock.release()
     print(value)# 在不加锁的情况下此时得出的结果会出现问题
     
 
 if __name__ == '__main__':
     for i in range(2):
         t = threading.Thread(target=add_value)
         t.start()
```

注意：加锁之后必须释放锁，不然会形成死锁

### 生产者和消费者模式

生产者：获取数据

消费者：保存数据

### 队列

> 队列在爬虫中的使用：
>
> 1. 将爬取的URL存放到队列中，每次生产者进行爬取时，会从队列中取出URL进行请求
> 2. 将生产者爬取到的数据存放到队列中，消费者从队列中取出数据进行保存

```python
 # 导入队列（先进先出）
 from queue import Queue
 
 # 创建Queue对象
 q = Queue(maxsize=4)# maxsize代表队列中的最大容量
 
 # put()：向队列中添加元素 
 q.put(1)
 q.put(2)
 q.put(3)
 q.put(4)
 # q.put(5)
 # 注意：如果队列满了，再添加数据，程序不报错，而是进入阻塞状态（等待从队列中取出元素）
 
 # get()：取出队列中的元素
 print(q.get())
 print(q.get())
 print(q.get())
 print(q.get())
 # print(q.get())
 # 注意：如果队列空了，在获取数据，程序不报错，而是进入阻塞状态（等待箱队列中添加元素）
 
 # full()：判断队列是否为满，返回布尔值
 
 # empty()：判断队列是否为空，返回布尔值
```

### 案例

#### 腾讯招聘-单线程

```python
# 需求：获取腾讯招聘岗位信息前100页的内容，并保存至mongoDB数据库

# 安装：pip install pymongo

import requests,pymongo

# 1.建立连接
client = pymongo.MongoClient(host='127.0.0.1', port=27017) # host：主机号，port：连接的MongoDB的端口号
# 2.进入数据库
db = client['tencent'] # 如果有名为tencent的数据库就进入，没有就创建
# 3.进入集合
col = db['zhaopin']

# 定义基础url
base_url = 'https://careers.tencent.com/tencentcareer/api/post/Query'
# 定义参数字典
params  =  {
    'pageSize': 10,
    'language': 'zh-cn',
    'area': 'cn'
}
# 定义请求头
headers = {'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36'}
for page in range(1,6):
    params[ 'pageIndex'] = page
    # print('\n现在是第' +str(page) + '页============\n')
    # 发起请求，获取响应
    response = requests.get(url=base_url, headers=headers, params=params)
    Posts = response.json()['Data']['Posts']
    for post in Posts:
        dic = {}
        # 获取内容
        # 获取岗位内容
        RecruitPostName = post['RecruitPostName']
        # 获取招聘时间
        LastUpdateTime = post['LastUpdateTime']
        # 获取岗位要求
        Responsibility = post['Responsibility']
        # print(RecruitPostName, LastUpdateTime,Responsibility)
        dic['RecruitPostName'] = RecruitPostName
        dic['LastUpdateTime'] = LastUpdateTime
        dic['Responsibility'] = Responsibility
        # 4.插入数据
        col.insert(dic)

# 5.关闭数据库
client.close()
```

```shell
# 在shell中查询保存到MongoDB的数据

# 打开MongoDB
mongo 
# 查看所有数据库
show dbs 
# 进入或创建数据库
use tencent
# 查看所有的聚合
show tables 
#查询集合并格式化输出
db.zhaopin.find().pretty() 
# 单次显示20多条数据，输入it查看更多
it 
```

#### 腾讯招聘-多线程
