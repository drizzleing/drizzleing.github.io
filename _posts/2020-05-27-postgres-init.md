---
layout: post
title:  "Postgres的初始化和客户端工具"
date:   2020-05-25 21:34:06 +0800
categories: 技术研究
tag: Postgres
---

{:toc}

### Postgresql数据库入门系列之二：数据库的初始化和客户端工具篇
---

#### 1. 按照上一篇结尾的安装成功提示，使用pg_ctl命令启动Postgresql

```shell
apple@drizzledeMac-mini ~ % pg_ctl -D /usr/local/var/postgres start
waiting for server to start....2020-05-27 20:23:52.420 CST [1994] LOG:  starting PostgreSQL 12.2 on x86_64-apple-darwin19.3.0, compiled by Apple clang version 11.0.0 (clang-1100.0.33.17), 64-bit
2020-05-27 20:23:52.423 CST [1994] LOG:  listening on IPv6 address "::1", port 5432
2020-05-27 20:23:52.423 CST [1994] LOG:  listening on IPv4 address "127.0.0.1", port 5432
2020-05-27 20:23:52.424 CST [1994] LOG:  listening on Unix socket "/tmp/.s.PGSQL.5432"
2020-05-27 20:23:52.449 CST [1995] LOG:  database system was shut down at 2020-05-25 22:28:02 CST
2020-05-27 20:23:52.458 CST [1994] LOG:  database system is ready to accept connections
 done
server started
```

#### 2. 使用psql命令，创建了一个数据库用户postgres

```shell
apple@drizzledeMac-mini var % psql postgres
psql (12.2)
Type "help" for help.

postgres=# create user postgres superuser with password '123456';
CREATE ROLE
postgres=#
```
#### 3. 用pgAdmin工具连上了postgresql

不了解哪个客户端好用，就选择了官方的pgAdmin，本以为是客户端app打开就能用了

可没想到是个http服务，通过浏览器打开管理端进行数据库的操作的，不过网页的交互界面感觉还是不错的

通过Add New Server把数据库的连接参数配置上去，就可以连接上数据库进行增删改查的操作了

pgAdmin的下载地址：<https://www.pgadmin.org/download/>

---
#### 写在最后：

关于Jekyll又发现了两个小问题：1、图片怎么上传和引用的？2、toc目录怎么使用的？且听下回分解。
