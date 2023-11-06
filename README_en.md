GCSLaoLi: 为README.md生成英文说明

GitHub Copilot: # cockroachai

A simple app for account sharing. It's free but not open source for now.

## Features

* Automatic refresh of AccessToken
* Session isolation between users
* Blocking of some sensitive information
* 1:1 complete official website UI, supports official website networking, plugins, drawing and other functions
* Suitable for small groups or account merchants to share accounts

## Prerequisites

* A server not on a certain AI's blacklist
* An account of a certain AI
* Docker and Docker Compose installed

## Installation

1. Clone this repository

```bash
git clone https://github.com/cockroachai/cockroachai.git
```

2. Enter the directory

```bash
cd cockroachai
```

3. Modify the configuration file

```bash
vim config/config.yaml
```
Change REFRESHCOOKIE to your account's Cookie

Change USERTOKENS to user tokens, multiple can be used

You can visit [here](https://demo.xyhelper.cn/getsession) to get RefreshCookie

4. Start

```bash
./deploy.sh
```


## Docking with third-party account systems
Configure environment variables or in config.yaml
```yaml
OAUTH_URL: https://xxxxx.xxx.com/ouath
```

When this value is configured, the user login will POST the following data to this address
```
userToken: User Token
```

The user login interface should return json data
```json
{
    "code": 1,
    "msg": "Prompt message when login fails",
    "refreshCookie": "Refresh Cookie, optional"
}
```
Where code is 1 means login is allowed, other values mean login is not allowed

msg is the prompt message when login fails

refreshCookie is Refresh Cookie, optional, if not filled in, the locally configured Refresh Cookie will be used
```