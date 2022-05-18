## FQ教程
### 服务端搭建
#### V2Ray
##### 一键脚本
```
bash <(curl -sL https://s.hijk.art/xray.sh)

最新
wget -N --no-check-certificate https://raw.githubusercontent.com/veip007/scripts/master/xray.sh && chmod +x xray.sh && bash xray.sh
```
- 配置文件在 /usr/local/etc/xray/ 下  
- 需要每三个月更新一下证书，证书位置在 /usr/local/etc/xray/ 下  
- nginx配置文件在 /etc/nginx/conf.d 下
- 伪装网站位于 /usr/share/nginx/html 下  

#### Trojan
##### 一键脚本
```
bash <(curl -sL https://s.hijk.art/trojan-go.sh)
```
- 配置文件在 /etc/trojan-go/ 下  
- 需要每三个月更新一下证书，证书位置在 /etc/trojan-go/ 下  
- nginx配置文件在 /etc/nginx/conf.d 下
- 伪装网站位于 /usr/share/nginx/html 下  

#### SSL证书问题
使用cloudflare中转流量：
1. 选“full(strict)模式
2. 加速选项页面，把auto minify里面勾选上：（javascipt、css、html），brotli开启。
3. 小云朵开启。

使用cloudflare自带的15年源证书就可以，然后选full(strict)模式使用它的边缘证书（一年期，会自动续期），打开Always Use HTTPS，这样就可以不用3个月去更新证书。然后把上面一键脚本安装后带的crontab注释掉。

### OpenWrt设置
- 接口Lan中网关和DNS全部改为主路由地址：192.168.50.1
- 忽略此接口的DHCP
- 设置PASSWALL，增加节点，打开主开关，有多个节点时打开自动切换，模式选中国列表以外
- 防火墙有lan的打开**IP动态伪装**，取消勾选**启用 SYN-flood 防御**
- 负载均衡：``` https://github.com/xiaorouji/openwrt-passwall/discussions/1820 ```

### iKuai设置
- 将需要翻墙的IP进行分组
- 设置端口分流：方式选下一跳网关，网关指向openwrt，源地址选择需要翻墙的设备组
- 认证计费里面可以选用不同的VPN协议方式，然后添加帐号密码，在端口分流里面选下一跳网关，同样能达到翻墙的目的

