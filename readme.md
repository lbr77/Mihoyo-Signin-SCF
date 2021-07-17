# Mihoyo sign in

![badge](https://github.com/jianggaocheng/mihoyo-signin/workflows/Mihoyo%20SignIn/badge.svg)

自动完成米游币任务
- 论坛区签到
- 阅读帖子
- 点赞帖子
- 分享帖子

## 更新记录 
[2020.11.16] 修复一时间后 cookie 失效的问题，重构部分代码以支持后期优化。

[2020.11.14] 感谢 [@lhllhx](https://github.com/lhllhx) 提醒，删除可能泄露 Cookie 的 log。

[2020.11.10] 重新加回本地运行的说明，修改了 cookie 的获取，重构代码加入随机延时防止检测。

[2020.11.02] 受 https://github.com/y1ndan/genshin-impact-helper 启发，支持 workflow 运行，每天 8 点定时进行签到。

## 快速入门

### 安装依赖
```
yarn
```

### 获取 cookie （一般来说只有初次运行需要，如 token 过期重做此步即可）
1, 登录 https://bbs.mihoyo.com/ys/, 如果已经登录需要退出再重新登录。

2, 在控制台输入以下指令, 取得 login_ticket, 并将结果复制
```javascript
var a=function getCookie(name){var strCookie=document.cookie;var arrCookie=strCookie.split("; ");for(var i=0;i<arrCookie.length;i++){var arr=arrCookie[i].split("=");if(arr[0]==name)return arr[1]}return""};console.log(a("login_ticket"));
```

3, 本地运行 cookie.js, 传入上一步的 login_ticket, 获取用于爬虫的 stoken
```bash
node cookie.js '*******第二步的login_ticket*******'
```

### 本地运行
在运行 cookie.js 的时候，控制台会返回一个 cookie string 的命令，直接拷贝到控制台继续运行即可
```bash
COOKIE_STRING='stuid=*******;stoken=****************;login_ticket=********************;' node index.js
```

### 腾讯云函数运行

1.下载包

2.新建函数，上传，环境选nodejs12.16,执行方法为serverless.handler

3.高级配置超时时间改为86400，打开异步执行，在环境变量中填入：

key: COOKIE_STRING, value: 上面得到的cookie string

4.配置触发器，自定义触发周期（建议`0 35 7 * * * *`）

5.测试

## 感谢

原项目[jianggaocheng/mihoyo-signin](https://github.com/jianggaocheng/mihoyo-signin)

受 https://github.com/lhllhx/miyoubi 项目启发  

感谢 https://github.com/lhllhx/miyoubi 的作者 [@lhllhx](https://github.com/lhllhx)  

感谢 [@2314933036](https://github.com/2314933036) 提供了签名 DS 字段的加密算法  
