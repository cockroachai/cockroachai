# cockroachai

[English](README_en.md)

一个简单的小程序，用于账号共享。免费但暂不开源。

## 功能

* 自动刷新AccessToken
* 用户间会话隔离
* 屏蔽部分敏感信息
* 1:1完全官网UI，支持官网联网，插件，绘图等功能
* 适合小团体或号商共享账号使用

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

可以访问 http://服务器IP:9000/getsession 获取RefreshCookie

4.启动

```bash
./deploy.sh
```
## 文件服务代理

因官方文件服务屏蔽了文件服务的境内访问权限，要想正常上传文件及显示生成的图片，需要对文件服务器进行代理。

通过配置文件参数或环境变量可以修改代理服务地址

默认为 
```yaml
FILESERVER: https://files.xyhelper.cn
```

## 对接第三方账户体系
配置环境变量或在config.yaml中配置
```yaml
OAUTH_URL: https://xxxxx.xxx.com/ouath
```

当该值被配置后，用户登陆时将向该地址POST以下数据
```
userToken: 用户Token
```

允许用户登陆接口应返回json数据
```json
{
    "code": 1,
    "msg": "登陆失败时的提示信息",
    "refreshCookie": "刷新Cookie，可选"
}
```
其中code为1时表示允许登陆，其他值表示不允许登陆

msg为登陆失败时的提示信息

refreshCookie为刷新Cookie，可选，如果不填写则使用本地配置的刷新Cookie

## 跳转登陆

访问 

```
http://服务器IP:9000/logintoken?access_token=xxxx
```

xxxx 为可用的userToken