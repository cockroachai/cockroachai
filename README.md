# cockroachai

一个简单的小程序，用于账号共享。免费但暂不开源。

## 功能

* 自动刷新AccessToken
* 用户间会话隔离
* 屏蔽部分敏感信息

## 前置要求

* 一台不在某AI黑名单的服务器
* 一个某AI的账号
* 安装好了Docker和Docker Compose

## 安装方法

1.克隆本仓库

```bash
git clone https://github.com/cockroachai/cockroachai.git
```

2.进入目录

```bash
cd cockroachai
```

3.修改配置文件

```bash
vim config/config.yaml
```
修改 REFRESHCOOKIE 为你的账号的 Cookie

修改 USERTOKENS 为用户Token，可以使用多个

可以访问 [这里](https://demo.xyhelper.cn/getsession) 获取RefreshCookie

4.启动

```bash
./deploy.sh
```