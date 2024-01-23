# cockroachai

[English](README_en.md)

一个简单的小程序，用于账号共享。免费但暂不开源。

交流群: https://t.me/xyhelper

## 重要提示

20231212 破坏性更新

1. 本次更新调整了数据库结构,以适应后期更进一步程序功能完善
2. 示例中提供了 mysql 配置示例,支持多实例共用同一数据库
3. 本次更新会话表名由`conversation`更改为`conversations`,如需保留原有会话,请手动迁移。

更新方法

1. 修改 config.yaml 增加配置

```yaml
cool:
  autoMigrate: true # 自动建表开关
```

2. 执行`./deploy.sh` 完成更新

## 功能

- 自动刷新 AccessToken
- 用户间会话隔离
- 屏蔽部分敏感信息
- 1:1 完全官网 UI，支持官网联网，插件，绘图等功能
- 适合小团体或号商共享账号使用

## 演示

演示站点提供了部分免费的 PLUS 账号，输入任意 6 位以上 userToken 即可登陆。为了避免滥用，演示站使用 4.0 模型时需人机验证。

[访问演示站点](https://xyhelper.cn/xq)

## 前置要求

- 一台不在某 AI 黑名单的服务器
- 一个某 AI 的账号
- 安装好了 Docker 和 Docker Compose

## 主机商推荐区

- 黑果云: https://www.hgidc.cn 国内持证商家，请咨询商家获取支持蟑螂的主机型号。

## 号商推荐区

| 序号 | xyhelper 群内名称                   | 可公布网站或其他联系方式                                                    | 业务范围                                                                                                  |
| ---- | ----------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 1    | 成本                                | 一般联系微信：LifelongJigsaw 或者 tg @chesterccj1                           | 正规代充 / 个人 Plus 拼车 / 自组拼车。优惠不超卖。                                                        |
| 2    | visa 开卡，💲 代付 GPT 全资源供应商 | qq2712057416                                                                | 正规充值号/退款流/api/各类代充/虚拟信用卡/国外实体信用卡等                                                |
| 3    | 西瓜君                              | qq2248200349                                                                | 正规充值号，手动充值/api/代充等                                                                           |
| 4    | chatgpt                             | qq:1498484059                                                               | 正规充值号/退款流/代充                                                                                    |
| 5    | fk.lqqq.ltd                         | [https://fk.lqqq.ltd](https://fk.lqqq.ltd)                                  | 普通/快速 5 刀号 api 批发                                                                                 |
| 6    | ChatGPT 代售（K）                   | QQ：1224478                                                                 | 出租或出售 Chat GPT 官方各种 API 额度和组织（纯一收货源）                                                 |
| 7    | cdw                                 | 15880283175                                                                 | 正规充值号/api/代充                                                                                       |
| 8    | Bruce                               | 微信：look6785                                                              | 专业正规代充/apikey 接口                                                                                  |
| 9    | 终章                                | [https://rao2-daili.hf.space/](https://rao2-daili.hf.space/)；QQ:2507838878 | 正规充值或成品号/api/各类代充等，手工代注册                                                               |
| 10   | tobemyslf                           | tobemyslf                                                                   | 正规 plus 售后 30 天/API 中转                                                                             |
| 11   | 雨葛葛                              | 15706745520                                                                 | 正规充值号/api/代充代付等。营业时间：9:00am-2:00am                                                        |
| 12   | Lucky Wang                          | [https://faka.aisvip.top](https://faka.aisvip.top) QQ：2643589579           | 五刀普号/0 刀普号，GPT 协议注册机/GPT 软件定制等                                                          |
| 13   | 超低价直连额度                      | duckgpt007                                                                  | 直连 api 一 💲0.6 元，有量有价                                                                            |
| 14   | 吴宾                                | 15604163368                                                                 | gpt 普号、plus 成品号和代充值，mj 成品号和代充值，一手退款流 plus，黑 plus，黑 mj，各业务零售批发都可来谈 |

注：

1. 排名不分先后，无参考价值。
2. 本站仅为群友征集整理公示，不参与任何利益关系，卖买双方自行洽谈，本站不对任何交易负责！

## 安装方法(本机部署)

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

配置管理员密码 ADMIN_PASSWORD: xxxxxxxx

修改 USERTOKENS 为用户 Token，可以使用多个

访问 http://服务器 IP:9000/getsession 输入官网账号密码及管理员密码写入 session.json

4.启动

```bash
./deploy.sh
```

## 安装方法(Docker)

1.安装Docker

```bash
wget -qO- get.docker.com | bash && systemctl enable docker  # 设置开机自动启动
```

2.安装Docker-compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

3.创建安装目录(可自行更改为所需目录)

```bash
mkdir -p /root/cockroachai && cd /root/cockroachai
```
```bash
vim docker-compose.yml
```

```bash
version: '3'
services:
  cockroachai:
    image: xyhelper/cockroachai:latest
    restart: always
    ports:
      - "9000:9000" #左侧端口暴露在外,可根据需求更改
    volumes:
      - ./config:/app/config
    environment:
      ASSET_PREFIX: https://oaistatic-cdn.closeai.biz  
```
按一下 esc，然后 :wq 保存退出

4.获取refreshtoken(针对第三方登录用户)


首先在电脑端打开https://chat.openai.com/api/auth/session (打开前确保你已在chat.openai.com登录)

然后按F12 点击应用 获取cookie 即名为"__Secure-next-auth.session-token"的值

然后打开当前目录下的config文件夹 创建配置文件(不创建配置文件将导致容器无法启动)
```bash
cd config && vim config.yaml
```

根据需求修改下述配置 并填写sessiontoken

```bash
# 以下配置兼容环境变量设置,配置文件优先级高于环境变量
# PROXY: "" # 代理地址 默认值 "",支持http https socks5
REFRESHCOOKIE: "（将你获取的sessiontoken输入到此 记得删除括号内内容）" # 刷新cookie,目前版本不再推荐使用,账号密码登录用户直接从getsession接口写入账号信息 默认值 ""
# OAUTH_URL: https://xxxxx.xxx.com/ouath # oauth地址 用于集成第三方登录 默认值 ""
# LOGIN_CALLBACK: "/login" # 登录回调地址,用于指定自己的登录页面 默认值 "/login"
# ASSET_PREFIX: https://oaistatic-cdn.closeai.biz # 静态资源前缀,用于指定自己的静态资源地址 默认值 https://oaistatic-cdn.closeai.biz
# ARKOSE_URL: https://tcr9i.closeai.biz/v2/ # arkose地址,用于指定自己的arkose人机验证地址 默认值 https://tcr9i.closeai.biz/v2/
# ADMIN_PASSWORD: xxxxx # 管理员密码 默认值为随机字符串,每次启动都会变化，可以在启动时通过日志查看，也可以指定一个固定值，方便管理
# AUDIT_LIMIT_URL: https://auditlimit.closeai.biz/audit_limit # 审计限制url 默认值 ""

# 以下配置不兼容环境变量设置,只能通过配置文件设置
USERTOKENS: # 用户token,可配置多个,本项内容支持热更新,更改后即时生效
  - "user1"
  - "user2"

# PROXY: "http://127.0.0.1:31280"  # 代理地址
# OAUTH_URL: https://xxxxx.xxx.com/ouath

# 注意注意,以下为新增配置,如需自动创建数据库,必加以下配置
cool:
  autoMigrate: true


# sqlite数据库配置
database:
  default:
    type: "sqlite" # 数据库类型
    name: "./config/cool.sqlite" # 数据库名称,对于sqlite来说就是数据库文件名
    extra: busy_timeout=5000 # 扩展参数 如 busy_timeout=5000&journal_mode=ALL
    createdAt: "create_time" # 创建时间字段名称
    updatedAt: "update_time" # 更新时间字段名称
    # debug: true # 开启调试模式,启用后将在控制台打印相关sql语句

# mysql数据库配置

# database:
#   default: # 数据源名称,当不指定数据源时 default 为默认数据源
#     type: "mysql" # 数据库类型
#     host: "127.0.0.1" # 数据库地址
#     port: "3306" # 数据库端口
#     user: "root" # 数据库用户名
#     pass: "xxxxxxxxx" # 数据库密码
#     name: "cockroachai" # 数据库名称
#     charset: "utf8mb4" # 数据库编码
#     timezone: "Asia/Shanghai" # 数据库时区
#     # debug: true # 是否开启调试模式，开启后会打印SQL日志
#     createdAt: "createTime" # 创建时间字段
#     updatedAt: "updateTime" # 更新时间字段
```

按一下 esc，然后 :wq 保存退出

5.运行
```bash
cd .. && docker-compose up -d
```



## 对接第三方账户体系

配置环境变量或在 config.yaml 中配置

```yaml
OAUTH_URL: https://xxxxx.xxx.com/oauth
```

当该值被配置后，用户登陆时将向该地址 POST 以下数据

```
userToken: 用户Token
```

允许用户登陆接口应返回 json 数据

```json
{
  "code": 1,
  "msg": "登陆失败时的提示信息",
  "refreshCookie": "刷新Cookie，可选"
}
```

其中 code 为 1 时表示允许登陆，其他值表示不允许登陆

msg 为登陆失败时的提示信息

refreshCookie 为刷新 Cookie，可选，如果不填写则使用本地配置的刷新 Cookie

## 跳转登陆

访问

```
http://服务器IP:9000/logintoken?access_token=xxxx
```

xxxx 为可用的 userToken

## 指定登陆页面地址

配置环境变量或在 config.yaml 中配置

```yaml
LOGIN_CALLBACK: "/login"
```

当用户退出或登陆失效后会跳转到该页面。

## 如何开设免费公益服务器

配置环境变量或在 config.yaml 中配置

```yaml
OAUTH_URL: http://127.0.0.1:9000/oauth
```

配置完成后重启服务，用户即可输入任意 6 位以上 token 完成登陆

## 关于 session.json

cockroachai 在运行过程中，会将账户 session 信息记录到 session.json 文件。在应用重启后，如果发现存在 session.json 文件，将会优先使用 session.json 中的账号信息。

手动修改 session.json 内容，可以将 /getsession 返回结果完整复制到该文件中保存。

在配置了正确的 session.json 后，可以不配置 refreshCookie.

## 静态文件服务

为了避免多实例重复加载字体,js,css 文件，可以配置环境变量或在 config.yaml 中配置

```yaml
ASSET_PREFIX: https://xxxxx.com
```

默认为 https://oaistatic-cdn.closeai.biz

部署静态文件服务的方法请参考仓库 https://github.com/cockroachai/cdn-oaistatic

## 内容审核及限速服务

如果有内容审核及限速(例如限制 3 小时 20 条)，可以配置限速服务接口

```yaml
AUDIT_LIMIT_URL: http://127.0.0.1:9612/audit_limit # 修改为你的审计限制接口url
```

不配置该项则不进行审计及限制

可参考示例审核服务。 https://github.com/cockroachai/auditlimit

## 如何更新

新版本镜像采用 docker 发布，可在程序安装目录执行 ./deploy.sh 进行更新，如有新版本发布，该命令会自动拉取新版本并重启服务。

## 如何重启服务

在程序安装目录执行

```bash
docker compose down
./deploy.sh
```
