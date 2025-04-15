# 手把手教你搭建轻量化 Minecraft Paper 1.20.2 服务器

> 本文最后更新于352天前，部分内容可能已过时。建议结合最新技术文档进行参考。

## 前言：为什么选择轻量化开服方案

在之前的教程中，我们已经介绍过多种Minecraft服务器搭建方式，包括使用翼龙面板和MCSM面板等方案。虽然这些第三方控制面板能简化操作流程，但它们会占用额外的服务器资源，对于内存有限的VPS来说并不理想。

本教程将详细演示如何从零开始搭建一个基于Paper 1.20.2的轻量化插件服务器，特别适合2-4GB内存的云服务器环境。

## 服务器配置选择指南

### 硬件配置建议
- **CPU**：建议至少2核（演示使用R9-5900X）
- **内存**：4GB足够支持10-20人同时在线
- **存储**：SSD硬盘至少20GB
- **网络**：NAT网络即可，后续通过端口映射解决

👉 [【点击查看】2025年最新雨云优惠码及特价云服务器方案汇总](https://bit.ly/RainYun)

### 系统环境准备
推荐使用Debian 11系统，执行以下命令更新系统：
bash
apt update -y && apt upgrade -y

## Java环境配置详解

### 安装Java 17
bash
apt install openjdk-17-jdk -y

### 验证安装
bash
java -version

正常应显示类似输出：

openjdk version "17.0.8" 2023-07-18

### 环境变量设置（如需要）
1. 查找Java安装路径：
bash
whereis java

2. 编辑profile文件：
bash
vim /etc/profile

3. 修改JAVA_HOME路径后保存退出

## Paper服务端部署流程

### 创建专用目录
bash
mkdir ~/mc && cd ~/mc

### 下载Paper 1.20.2
bash
wget https://api.papermc.io/v2/projects/paper/versions/1.20.4/builds/365/downloads/paper-1.20.4-365.jar

## 服务器初始化配置

### 首次启动
bash
java -jar paper-1.20.4-365.jar nogui

### 同意EULA协议
1. 编辑eula.txt文件
2. 将`eula=false`改为`eula=true`

### 关键配置修改
编辑server.properties文件：
properties
motd=我的专属服务器
difficulty=normal
max-players=20
online-mode=true
view-distance=8

## 服务器管理技巧

### 使用screen保持会话
bash
screen -S mc
java -jar paper-1.20.2-280.jar nogui

退出会话：`Ctrl+A+D`

### 端口映射设置
将内网25565端口映射到外网端口，具体操作根据云服务商控制面板进行。

## 连接服务器指南
在Minecraft客户端中添加服务器时使用：

外网IP:映射端口

> 提示：建议定期备份world文件夹，并考虑安装基础权限管理插件提升安全性。