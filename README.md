# cockroachai

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

可以访问 [这里](https://demo.xyhelper.cn/getsession) 获取RefreshCookie

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
}
```
其中code为1时表示允许登陆，其他值表示不允许登陆