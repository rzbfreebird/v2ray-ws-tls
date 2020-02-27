### 原作者：
* https://github.com/atrandys/v2ray-ws-tls

# v2ray-ws-tls一键安装脚本： 

* 此脚本是v2ray使用websocket+tls自由上网的方法，虽然此方法稍微复杂，速度慢一些，但稳定性较好，不易被Q，追求稳定可以尝试。

# 目录介绍：

* v2ray_ws_tls           安装脚本
* v2ray_ws_tls_with_wp   wordpress+v2ray+websocket+tls安装脚本
* v2ray_ws_tls1.3        安装脚本
* web                    网站文件  

# 说明：

* 1.一键脚本需要VPS安装为CentOS7系统
* 2.本方案需要一个域名并解析到你的VPS的IP，随便买个一刀以内的便宜域名，或者可以去 www.freenom.com 申请免费域名
* 3.当前版本v2ray不支持TLS1.3，当v2ray支持后，本次一键搭建的服务端可升级支持
* 4.搭配bbr加速，可以让速度有较大的提升
* 5.一键脚本会为你配置一个英文模板的网站，你也可以自行替换自己的网页

# 安装教程：     

* 1.执行下面的命令安装v2ray+ws+tls
``` bash
curl -O https://raw.githubusercontent.com/rzbfreebird/v2ray-ws-tls/master/v2ray_ws_tls.sh && chmod +x v2ray_ws_tls.sh && ./v2ray_ws_tls.sh
```
* 2.等待脚本执行，过程中会提示需要输入域名，输入解析到本VPS的域名，然后回车
* 3.等待安装完成，你可以看到配置参数，客户端配置时用到，如果不小心忘记了可以输入下列代码重新查看
``` bash
cat /etc/v2ray/myconfig.json
```
* 4.安装BBR加速（可不安装，或自行开启bbr）
``` bash
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/rzbfreebird/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
* 4.注意在弹出的安装界面首先选择` 1 `，安装BBR内核,安装过程可能时间较长,耐心等待
* 5.安装完成后会提示重启VPS,输入` Y `，然后回车，确认重启。然后等待几分钟，再使用xshell连接vps（连接方法是点软件上重新打开，找到之前保存的连接，点连接）登陆后执行下列命令
``` bash
cd /usr/src && ./tcp.sh
```
* 6.在弹出安装界面,输入` 5 `,然后回车，使用BBR魔改版加速，等待安装完成提示bbr启动成功即可

# 客户端配置：

* 1.下载v2ray客户端,v2ray各平台客户端：https://www.v2ray.com/awesome/tools.html
* 2.将参数对应填写到客户端,这里大概说明一下参数怎么填写：地址：你的域名，例如google.com;端口：443;用户ID：就是一长串uuid;加密方式：aes-128-gcm;传输协议：ws;path：就填路径这个参数;底层传输：tls
* 3.开启上网即可
* 4.关于移动端说明。这个方案下，有的客户端可用有的不可用，那么需要你在保证配置正确的情况下，多试几个客户端

# 伪装网站配置：

脚本已经创建好了一个英文模板站，如果你想自己为VPS配置一个其他的伪装站点，可自行获取网页文件，入口页包含index.html，将其传输到VPS的/etc/nginx/html目录下，重启VPS即可

# 域名套CDN：

* 1.套CDN需要在以上教程搭建完成的基础上进行
* 2.自行寻找供应CDN服务的网站，这里提供一个免费CDN的网址：https://www.cloudflare.com/
* 3.根据对应CDN网站调整域名解析设置
* 4.等待CDN生效，v2ray的参数不需要任何修改
* 5.套CDN只是让IP可以隐藏起来，从而被Q的难度降到最低，但是对于大多数地区，套了CDN后访问的速度会变慢很多，所以是否套CDN还请自行判断