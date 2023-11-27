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

也可以访问 https://cockroachai.xyhelper.cn/getsession  获取RefreshCookie

4.启动

```bash
./deploy.sh
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

## 指定登陆页面地址
配置环境变量或在config.yaml中配置
```yaml
LOGIN_CALLBACK: "/login"
```
当用户退出或登陆失效后会跳转到该页面。
## 如何开设免费公益服务器
配置环境变量或在config.yaml中配置
```yaml
OAUTH_URL: http://127.0.0.1:9000/ouath
```
配置完成后重启服务，用户即可输入任意6位以上token完成登陆

## 关于session.json
cockroachai在运行过程中，会将账户session信息记录到  session.json文件。在应用重启后，如果发现存在session.json文件，将会优先使用session.json中的账号信息。

手动修改session.json内容，可以将 /getsession 返回结果完整复制到该文件中保存。


在配置了正确的session.json后，可以不配置refreshCookie.

## 如何更新

新版本镜像采用docker发布，可在程序安装目录执行  ./deploy.sh 进行更新，如有新版本发布，该命令会自动拉取新版本并重启服务。

## 如何重启服务

在程序安装目录执行
```bash
docker compose down
./deploy.sh
```