# 微信企业号



---

###一.申请企业号
1. 以个人邮箱申请就可以, 不通过企业认证的话,有200人的限制,一般足够用了

###二.获取对接权限
1. 获取corpid
    登录后,左侧菜单[设置] ----> 右侧帐号信息的 CorpID
    将 CorpID 配置到配置文件 config.conf 内,在有公网IP运行的机器上运行,可以被外部访问
2. 开启回调模式获取key
    登录后,左侧菜单[应用中心] ----> 自建应用 ----> 企业小助手 --->模式选择 ----> 回调模式
    > * URL: 填写你服务器地址:端口/wxauth( 例如: http://yanjunhui.com:4567/auth )
    > * Token: 随机获取(这个发送信息用不到,可忽略)
    > * EncodingAESKey: 随机获取,就是我们在配置文件配置的 key

3. secret
    登录后,左侧菜单 [设置] ----> 权限管理
    > 1. 新建一个普通管理组, 
    > 2. 设置一个管理员(需要另外一个已经关注企业号的微信帐号)
    > 3. 应用权限,设置应用中心的[企业小助手]
    > 4. 通讯录权限,全部勾选即可
    生成的Secret就是我们需要的 secret


###完成以上步骤后, 即可实用OpenFalcon发送信息,发送格式与 sender 符合:
    tos     微信用户名
    content 信息内容
    

OpenFalcon+:

修改配置文件 https://github.com/open-falcon/falcon-plus/blob/master/modules/alarm/cfg.example.json#L25

```
"api": {
        "sms": "http://yanjunhui.com:4567/send",
        "mail": "http://127.0.0.1:10086/mail",
        "dashboard": "http://127.0.0.1:8081",
        "plus_api":"http://127.0.0.1:8080",
        "plus_api_token": "used-by-alarm-in-server-side-and-disabled-by-set-to-blank"
    },
```





1. 如果只需要微信提醒, 只修改 OpenFalcon 的 Sender 的配置文件 sms 的地址: http://IP:4567/sendmsg:
	例如:

```
    "api": {
        "sms": "http://yanjunhui.com:4567/send",
        "mail": "http://11.11.11.11:9000/mail"
    }
```


2. 如果同时需要短信和微信提醒,可以使用修改版的[Sender](https://github.com/Yanjunhui/sender),配置如下:
```
    "api": {
        "sms": "http://11.11.11.11:8000/sms",
        "mail": "http://11.11.11.11:9000/mail"
        "chat": "http://11.11.11.11:4567/send"
    }
```
