
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
