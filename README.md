# UptimeRobot 状态监测页

> 一款基于 [UptimeRobot](https://uptimerobot.com/) 中文状态监测页

[![Docker Build Status](https://img.shields.io/docker/build/giuem/uptimerobot-page.svg?style=flat-square)](https://hub.docker.com/r/nangle/status-page/)
[![license](https://img.shields.io/github/license/XOS/StatusPage.svg?style=flat-square)](https://github.com/XOS/StatusPage/blob/master/LICENSE)

## 修改说明
* 前端改为中文显示；
* 改变页面显示宽度；
* 修改显示数据为最近 60 天（原版 45 天）；
* 增加显示当前日期数据（原版只显示到前一天）；
* Docker 环境时修改时区为东八区；
* 其它布局微调

## 效果展示

![](https://cdn.jsdelivr.net/gh/XOS/StatusPage@master/status.nange.cn.png)

## 常规环境下部署使用
```bash
git clone https://github.com/XOS/StatusPage.git && cd StatusPage
npm i
yarn install && yarn cache clean
yarn build
```
修改 config/default.yml
```bash
node build/bootstrap
```

## Requirements

* Node.js >= 10
* Uptime Robot API key
* Docker and docker-compose (optional)

## Docker 环境下部署使用

```bash
wget https://raw.githubusercontent.com/XOS/StatusPage/master/docker-compose.yml
docker-compose up -d
```

## Configure

There are two ways to configure:
* config files in `config/*.yml`
* environment variables (map: [config/custom-environment-variables.yaml](config/custom-environment-variables.yaml))

The file loading order is **default.yml < ${NODE_ENV}.yml < environment variables**.
It's recommend to set secrets (e.g. API key) via environment variables and something complex (e.g. array and object) via files.

## Parser Usage

We use the parser to analyze groups name, monitors name and group index (optional) which included in your original monitor's name. 
Default Parser is `%group/%name`, there are 3 variables now: 
  - %group
  - %name
  - %index 

You can change the backslash / to any separator you like, as long as it won't used in your group & monitor name (and index). 
To put index into your parser, you will able to sort your group in page manually. Easily write index for each group once (also for all if you like), and leave the blank of the index for other monitors in the same group.

> There is example:
> **Group Name**/**Index**/**Monitor Name**
> ```
> %group/%index/%name
> ```
> For this format, you should write index in original name at Uptimerobots Control Panel for each group once:
> ```
> GroupA/1/MonitorA
> ```
> And leave the blank of the index for other monitors in the same group.
> ```
> GroupA//MonitorB
> ```

