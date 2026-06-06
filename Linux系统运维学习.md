# Linux系统运维学习

## 第 1 周 Linux 基础命令

[周一](/Linux系统运维学习/第一周/周一.md)：VMware 装 CentOS→配静态 IP→FinalShell 远程连接

[周二](/Linux系统运维学习/第一周/周二.md)：ls cd pwd mkdir rmdir 目录实操

[周三](/Linux系统运维学习/第一周/周三.md)：touch rm cp mv 文件实操

[周四](/Linux系统运维学习/第一周/周四.md)：cat more less head tail 查看文件

[周五](/Linux系统运维学习/第一周/周五.md)：find grep 查找 + 过滤

周六：tar zip unzip 打包压缩

周日：本周命令全复盘，笔记传 GitHub

## 第 2 周 系统进阶｜权限 / 磁盘 / 进程 / YUM

周一：useradd userdel groupadd passwd 用户管理

周二：chmod chown chgrp 权限 + 属主属组

周三：df du mount umount 基础磁盘挂载

周四：虚拟机加硬盘→fdisk 分区→格式化→永久挂载

周五：ps top kill ss 进程 + 端口排查

周六：换 YUM 国内源，yum 安装卸载软件

周日：复盘磁盘、权限、进程实操

## 第 3 周 网络 + 防火墙 + 日志

周一：吃透 IP / 网关 / 子网掩码 / TCP 三次握手

周二：ping curl traceroute 网络命令实操

周三：firewalld 放行 80、3306 端口，配置规则

周四：iptables 基础规则查看与清空

周五：systemctl 服务自启、启停管理

周六：/var/log 系统日志、安全日志查看排错

周日：重配防火墙，口述网络知识点

## 第 4 周 LNMP 手动服务搭建

周一：YUM 安装 Nginx，启动 + 开机自启 + 浏览器访问

周二：Nginx 配置多虚拟主机

周三：安装 MySQL、设密码、登录数据库

周四：MySQL 建库、建用户、授权、基础备份

周五：安装 PHP，配置 Nginx 解析 PHP

周六：完整 LNMP 打通，访问测试页

周日：不看笔记，独立重装一遍 LNMP

## 第 5 周 Shell 入门

周一：Shell 变量、echo，写脚本输出主机名 + IP

周二：if 判断，脚本不存在目录自动创建

周三：for 循环，批量创建 10 个用户

周四：while 循环，1-100 循环输出

周五：函数封装，系统信息函数调用

周六：sed 基础替换配置文件内容

周日：所有脚本整理，提交 GitHub

## 第 6 周 Shell 运维实用脚本

周一：系统巡检脚本（CPU / 内存 / 磁盘 / IP）

周二：磁盘使用率监控告警脚本

周三：批量删除用户脚本

周四：awk 分析 Nginx 日志，统计访问量

周五：Nginx 日志自动清理（保留 7 天）

周六：crontab 定时任务配置所有脚本

周日：调试脚本，优化注释

## 第 7 周 Shell 项目收尾｜简历项目 1 完工

周一：MySQL 自动备份脚本（压缩 + 保留 30 天）

周二：Nginx/MySQL 服务监控告警脚本

周三：全局调试所有脚本，修复 Bug

周四：写项目使用文档

周五：脚本运行截图、整理目录结构

周六：完善 GitHub 项目介绍

周日：✅ 简历项目 1：Shell 自动化脚本集定稿

## 第 8 周 Ansible 入门

周一：3 台机器配置 SSH 免密登录

周二：主控安装 Ansible，配置 inventory 主机清单

周三：ad-hoc 批量执行命令，查磁盘、建文件

周四：学习 yum、copy、file 模块实操

周五：学习 service、user 模块实操

周六：批量给被控机建用户、装软件

周日：复盘所有常用模块用法

## 第 9 周 Ansible Playbook 基础

周一：学 YAML 语法、Playbook 结构

周二：Playbook 批量安装 Nginx

周三：Playbook 推送 Nginx 配置文件

周四：Playbook 服务器初始化（关防火墙 + 同步时区）

周五：Playbook 批量启停服务

周六：执行 Playbook 理解幂等性

周日：所有 Playbook 提交 GitHub

## 第 10 周 Ansible 综合项目｜简历项目 2 完工

周一：编写服务器一键初始化 Playbook

周二：编写一键批量部署 LNMP Playbook

周三：模块化拆分 Playbook，可复用

周四：3 台机器完整一键部署跑通

周五：项目截图、编写项目文档

周六：优化 GitHub 仓库，梳理项目亮点

周日：✅ 简历项目 2：Ansible 自动化平台定稿

## 第 11 周 Docker 容器化｜简历项目 3 完工

周一：安装 Docker，掌握镜像 / 容器基础命令

周二：拉取 Nginx、MySQL 镜像，运行容器

周三：编写 Dockerfile，定制 Nginx 私有镜像

周四：学习 docker-compose 语法

周五：Compose 编排 Nginx+MySQL+WordPress

周六：数据卷挂载，实现博客数据持久化

周日：截图写文档传 GitHub，✅ 简历项目 3 定稿

## 第 12 周 求职冲刺｜简历 + 面试 + 投实习

周一：整理 3 个项目截图、GitHub 链接、项目素材

周二：按模板写完运维实习简历

周三：刷 Linux 基础、权限、磁盘面试题

周四：刷 Shell、脚本、crontab 面试题

周五：刷 Ansible、Docker、网络面试题

周六：完整口述 3 个项目流程和亮点

周日：投递 Linux 运维 / 云计算运维实习