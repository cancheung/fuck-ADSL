﻿![拓扑图](fuck-ADSL.png)
国内ADSL不能搭建服务器，大家都懂，只能曲线救国
===
- 此工程为了解决我访问家里摄像头问题。
- 家中服务器开放端口监听后，时不时会被ADSL断一下网，而且数据100%不能收到。使用本地IP测试没问题的。
- 估计ADSL在所在地区的交换机作扫描，发现有监听端口就断你网，并把进入的数据包直接截掉。

Why
----
截止今天，网上能买到的网络摄像头都是要把视频/国像数据传输到厂商服务器的，
用户再从厂商服务器读取视频；带来问题：
- 延迟严重
- 长期占用家中带宽
- 私隐安全问题

How 如何实现
----
1. 必需有台固定IP的外网服务器作中转。称为SVR，IP为：123.123.123.123
2. 在SVR中跑程序 svr_main.go, 使用--help查看参数。假定监听 8080与8081
2. 家里跑一台Linux服务器，我使用[Raspberry-Pi](https://github.com/toontong/Raspberry-Pi),功耗低。称为Pi,IP: 192.16.1.110
3. 在Pi中跑 [mjgp-streamer](https://github.com/toontong/mjpg-streamer)，端口为8080
4. 在Pi中跑 cli_main.go, 使用 --help查看参数。
5. 此时访问 http://123.123.123.123:8080/ 就如访问内网的mjpg-streamer。

已实现：
----
http与ssh级别的数据中转。

TODO:
-----
- web-admin控制客户端。
- 单元测试