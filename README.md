## 介绍

一个非常简单的前后端分离项目

这个项目是一个基于 Vue 和 Django 的图书管理系统。它允许用户查看图书列表、添加新图书，并提供了一个简单的用户界面。

以下是项目的一些主要特点：

1. 使用 Vue 3 和 TypeScript 编写前端代码。
1. 使用 Django REST framework 编写后端 API。
1. 使用 Axios 库进行前后端通信。
1. 使用 Django 自带的 SQLite 数据库存储数据。

## 如何部署

1. 按常规方法分别安装front目录中vue的和back目录中python的依赖
1. 在front目录中运行

    ```bash
    yarn run build
    ```

1. 将front中生成的dist文件夹复制到back目录下
1. 在back目录中运行

    ```bash
    python manager.py runserver
    ```
