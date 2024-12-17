# AI 与程序员之间交互怎么样合理

## 充分利用 terminal

cursor 之类都增加了一个 chat 的聊天交互框，其实增加了很多东西，交互起来并不舒服，程序员天生会与 terminal 交互，那为什么不复用 terminal
terminal 的输入输出都可以被 AI 接管做中间过程处理，是一种更方便更简介的方式。

1. 人工输入 -> AI 预处理 -> Agent 执行

如，我在终端中输入:
```
$ 帮我创建个数据库
我即将帮你创建 pgsql 数据库，规格为 2CPU 4G内存 10G磁盘 三副本，是否确认？
$ 开发测试环境，单副本就行，其他没问题
创建中...
已完成
数据库信息为：
postgresql://postgres:q2nq2sl7@test-db-postgresql.ns-bxkx84bw.svc:5432
（该信息已经被录入上下文，编码时会自动取用这个值）
```

2. 程序输出 -> AI 后处理 -> Agent 执行

```
$ devbox@devbox:~/project$ python3 hello.py
Traceback (most recent call last):
  File "/home/devbox/project/hello.py", line 1, in <module>
    from flask import Flask, request, jsonify, render_template
ModuleNotFoundError: No module named 'flask'
```
当出现这样一段报错时，cursor 的选择是 add to chat，本身 terminal 为什么不能是 chat，而且我大概率是需要 AI 给我去解决这个问题的。
```
环境中没有安装 Flask 模块, 这就为您生成安装命令
$ pip install Flask
```
然后用户敲 enter 安装

3. 一些 read only 能发现的错误可以直接提示出来

举个例子，用户代码中的数据库地址和生成的数据库真实地址不匹配，在运行程序时可以提示出来。
再比如用户监听的端口号与 devbox 中配置的端口号不一致，也可以提示出来。

```
$ python hello.py
我检测到程序监听的端口号是 8080，而 devbox 暴露的端口是 3000，不一致，会导致外网域名无法访问。
```
