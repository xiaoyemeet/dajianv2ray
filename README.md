# hax白嫖
vps地址：https://hax.co.id/
centos7系统选KVM的VPS
视频教程：https://www.youtube.com/watch?v=-5F1KixFDbU&list=PLSue0ax5RxRp3SLl8kyiAAB0p4QLt3Wvf
文字教程：https://binghequanzi.blogspot.com/2021/12/vpshaxxray-x-uivmessvlesstrojanshadowso.html

映射三个端口：
22至91.134.238.133:7899（用于远程shh连接）
54321至91.134.238.133:7900
11885（面板里默认的端口）至91.134.238.133:7901

面板安装命令   bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)

面板用hax自己搭建的节点打不开

面板中按照默认的选项添加一条规则就可以使用

* 使用cloudflare：
cf中添加一条IPv6的DNS解析，指向服务器的v6地址
然后继续在ssl中添加一个客户端证书
面板中添加一条新规则：端口改为443，传输协议选为ws，启用tls，伪装域名即为指向服务器v6的地址，复制证书粘贴，其他默认即可！


# virmach搭建
vps地址：https://billing.virmach.com/
centos7系统
视频教程：https://www.youtube.com/watch?v=a4HTABfJp90&list=PLSue0ax5RxRp3SLl8kyiAAB0p4QLt3Wvf&index=49&t=714s
文字教程：https://do.445600.cf/?p=51
注意新购买的vps的账号密码会发到邮箱（登录端口22）

在cloudflare中添加一个DNS解析域名指向服务器的v4地址

安装wget：  yum install wget vim -y

机器跑分：wget -qO- --no-check-certificate https://raw.githubusercontent.com/oooldking/script/master/superbench.sh | bash

一键安装脚本：wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh"; && chmod +x install.sh && bash install.sh

安装中需要核对时间，输入上述域名，安装完会直接给出vmess链接地址，复制到v2ray客户端中添加即可

* 在cloudflare配置worker开启CDN：
先使用IP优选工具优选出一个IP
然后在worker中添加一个新的woker：
addEventListener(
"fetch",event => {
let url=new URL(event.request.url);
url.hostname="这里填上述域名";
let request=new Request(url,event.request);
event. respondWith(
fetch(request)
)
}
)

然后将该节点的地址改为cf的优选ip，伪装域名改为worker的地址，即可实现CDN加速！
