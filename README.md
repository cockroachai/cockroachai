# cockroachai

[English](README_en.md)

一个简单的小程序，用于账号共享。免费但暂不开源。

交流群: https://t.me/xyhelper

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


| 序号 | xyhelper群内名称      | 可公布网站或其他联系方式                               | 业务范围                                                       |
| ---- | ------------------ | -------------------------------------------------- | ----------------------------------------------------------- |
| 1    | 成本               | 一般联系微信：LifelongJigsaw或者tg @chesterccj1   | 正规代充 / 个人Plus拼车 / 自组拼车。优惠不超卖。                |
| 2    | visa开卡，💲代付GPT全资源供应商 | qq2712057416                                      | 正规充值号/退款流/api/各类代充/虚拟信用卡/国外实体信用卡等       |
| 3    | 西瓜君              | qq2248200349                                      | 正规充值号，手动充值/api/代充等                                |
| 4    | chatgpt            | qq:1498484059                                     | 正规充值号/退款流/代充                                         |
| 5    | fk.lqqq.ltd        | [https://fk.lqqq.ltd](https://fk.lqqq.ltd)        | 普通/快速5刀号api批发                                          |
| 6    | ChatGPT代售（K）   | QQ：1224478                                       | 出租或出售Chat GPT官方各种API额度和组织（纯一收货源）           |
| 7    | cdw                | 15880283175                                       | 正规充值号/api/代充                                            |
| 8    | Bruce              | 微信：look6785                                    | 专业正规代充/apikey接口                                        |
| 9    | 终章               | [https://rao2-daili.hf.space/](https://rao2-daili.hf.space/)；QQ:2507838878 | 正规充值或成品号/api/各类代充等，手工代注册                    |
| 10   | tobemyslf          | tobemyslf                                         | 正规plus售后30天/API中转                                       |
| 11   | 雨葛葛             | 15706745520                                       | 正规充值号/api/代充代付等。营业时间：9:00am-2:00am             |
| 12   | Lucky Wang         | [https://faka.aisvip.top](https://faka.aisvip.top) QQ：2643589579 | 五刀普号/0刀普号，GPT协议注册机/GPT软件定制等                  |
| 13   | 超低价直连额度      | duckgpt007                                        | 直连api一💲0.6元，有量有价                                     |

注：
1. 排名不分先后，无参考价值。			
2. 本站仅为群友征集整理公示，不参与任何利益关系，卖买双方自行洽谈，本站不对任何交易负责！



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

配置管理员密码 ADMIN_PASSWORD: xxxxxxxx

修改 USERTOKENS 为用户 Token，可以使用多个

访问 http://服务器 IP:9000/getsession 输入官网账号密码及管理员密码写入 session.json


4.启动

```bash
./deploy.sh
```

## 对接第三方账户体系

配置环境变量或在 config.yaml 中配置

```yaml
OAUTH_URL: https://xxxxx.xxx.com/ouath
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
OAUTH_URL: http://127.0.0.1:9000/ouath
```

配置完成后重启服务，用户即可输入任意 6 位以上 token 完成登陆

## 关于 session.json

cockroachai 在运行过程中，会将账户 session 信息记录到 session.json 文件。在应用重启后，如果发现存在 session.json 文件，将会优先使用 session.json 中的账号信息。

手动修改 session.json 内容，可以将 /getsession 返回结果完整复制到该文件中保存。

在配置了正确的 session.json 后，可以不配置 refreshCookie.

## 静态文件服务
为了避免多实例重复加载字体,js,css文件，可以配置环境变量或在 config.yaml 中配置

```yaml
ASSET_PREFIX: https://xxxxx.com
```
默认为 https://oaistatic-cdn.closeai.biz

部署静态文件服务的方法请参考仓库   https://github.com/cockroachai/cdn-oaistatic

## 如何更新

新版本镜像采用 docker 发布，可在程序安装目录执行 ./deploy.sh 进行更新，如有新版本发布，该命令会自动拉取新版本并重启服务。

## 如何重启服务

在程序安装目录执行

```bash
docker compose down
./deploy.sh
```
