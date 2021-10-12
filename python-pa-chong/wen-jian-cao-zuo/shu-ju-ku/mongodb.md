# MongoDB

> 数据在MongoDB中是按照“库（Database）”—“集合（Collections）”—“文档（Document）”的层级关系来存储的。 如果使用Python的数据结构来做类比的话，文档相当于一个字典，集合相当于一个包含了很多字典的列表，库相当于一个大字典，大字典里面的每一个键值对都对应了一个集合，Key为集合的名字，Value就是一个集合

## 安装MongoDB

pass---

## 安装RoboMongo

> RoboMongo是一个跨平台的MongoDB管理工具，可以在图形界面中查询或者修改MongoDB

### 使用RoboMongo

1. 如果数据库就在本地计算机，只需要在Name一栏随便取个名字即可
2. 单击“Connect”按钮连接MongoDB

## PyMongo的安装与使用

> PyMongo模块是Python对MongoDB操作的接口包，能够实现对MongoDB的增删改查及排序等操作

### 安装

```shell
pip install pymongo
```

### 使用

1. 初始化数据库
