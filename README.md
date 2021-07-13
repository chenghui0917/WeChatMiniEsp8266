
<p align="center">
  <img src="png/phone.png" width="400px" height="560px" alt="Banner" />
</p>
 

## 一、前言

  - 这是一个开源的可连接**非微信服务器**的```mqtt.js```的代码工程，本工程的配置文件如下图所示```index.js```，在里面修改为您的搭建好的MQTT服务器以及想要订阅的主题，想要连接更多关于微信小程序控制智能硬件（包括```esp8266、esp32```），包括，请移步：https://blog.csdn.net/xh870189248/article/details/84070944
  

  
## 二、版本迭代
|版本|更新说明|更新时间|
| :---- | :---- | :----- | 
|1|首次提交|2018-11-18|
|2| phao mqtt底层库移除，更换为 mqtt.js!修复稳定性问题！|2019-2-20|
## 三、特别注意

  - 还是要特别提醒，默认的是```443```端口！以及连接的链接不能带端口号！连接格式：```wsx:www.domain.com/mqtt```，不用带端口号！
  - 移植来自 https://github.com/mqttjs/MQTT.js 更多使用技巧访问其使用文档！或者阅读我本仓库提供的代码！共勉！
 
 ## 四、加群将免费提供服务器连接测试！
 
   - 福利多多，请加QQ群：434878850
 ---------------------------
 
 ![Alt text](png/screen.png)
 
 
 开源社区提供了小程序 MQTT 接入的 Demo：https://github.com/iAoe444/WeChatMiniEsp8266

(opens new window) 下载解压到一个文件夹后，用微信小程序开发者工具，打开 index.js 文件，将 MQTT 地址、用户名和密码改为实际参数即可。

按照以上 3 步的安装配置，你的微信小程序已经能够成功连接到 EMQ X 服务器了。


EMQ X MQTT 微信小程序接入

微信小程序支持通过 WebSocket 进行即时通信，EMQ X 的 MQTT Over WebSocket 能够完全兼容使用在微信小程序上。

TIP

由于微信小程序的规范限制，EMQ X 使用微信小程序接入时需要注意以下几点：

    必须使用已经通过域名备案

(opens new window)的域名接入
域名需要在小程序管理后台

    (opens new window)域名/IP 白名单中(开发 -> 开发设置 -> 服务器域名 -> socket 合法域名)
    仅支持 WebSocket/TLS 协议，需要为域名分配受信任 CA 颁发的证书
    由于微信小程序 BUG，安卓真机必须使用 TLS/443 端口，否则会连接失败（即连接地址不能带端口）

#
参考资料

    EMQ X 使用 WebSocket 连接 MQTT 服务器

(opens new window)
CSDN Nginx 反向代理 WebSocket
(opens new window)
微信小程序 MQTT 接入Demo

    (opens new window)

#
详细步骤

1、注册微信小程序帐号，并下载微信开发者工具

(opens new window)。由于微信小程序安全要求比较高，在与后台服务器之间的通讯必须使用 https 或 wss 协议，因此要在微信小程序后台设置域名服务器。

登录小程序后台后，找到 开发设置 -> 服务器域名 进行服务器配置，在 socket 合法域名处输入格式如 wss://xxx.emqx.io，此处不带端口号。

2、服务器端要申请并安装证书，华为云等云提供商均可以申请免费证书

(opens new window)。

这里必须注意的是，证书申请绑定时，必须与所使用的服务器域名一致，此处建议使用 Nginx 来做反向代理并终结证书，相关配置如下：

server {
    listen  443 ssl;        
    server_name xxx.emqx.io; 
    ssl_certificate   cert/***.pem;
    ssl_certificate_key  cert/***.key;
    ssl_session_timeout  5m;      
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;

    # 添加反向代理
    location /mqtt {
      proxy_pass http://127.0.0.1:8083/mqtt;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      # client_max_body_size 35m;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";    
    }

}

 

 
        Copied!
    

3、开源社区提供了小程序 MQTT 接入的 Demo：https://github.com/iAoe444/WeChatMiniEsp8266

(opens new window) 下载解压到一个文件夹后，用微信小程序开发者工具，打开 index.js 文件，将 MQTT 地址、用户名和密码改为实际参数即可。

按照以上 3 步的安装配置，你的微信小程序已经能够成功连接到 EMQ X 服务器了。
