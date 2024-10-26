# realm-oneclick-install

### 脚本用法
```
realm自助安装脚本
realm is a simple, high performance relay server written in rust.
项目地址：https://github.com/zhboner/realm

使用方法：bash realm.sh [-h] [-i] [-u]

  -h , --help                显示帮助信息
  -i , --install             安装realm
  -u , --uninstall           卸载realm
```

### 脚本安装的文件
```
installed: /usr/bin/realm
installed: /etc/systemd/system/realm.service
installed: /usr/local/etc/realm/config.toml
```

### 安装
```
bash <(curl -L https://raw.githubusercontent.com/zhouh047/realm-oneclick-install/main/realm.sh) -i
```

### 卸载
```
bash <(curl -L https://raw.githubusercontent.com/zhouh047/realm-oneclick-install/main/realm.sh) -u
```

### 注意
本脚本没有自动配置转发，也没有启动realm。

请编辑```/usr/local/etc/realm/config.toml```，添加转发配置。
配置示例
```
# 最简配置
[[endpoints]]
listen = "0.0.0.0:5000"
remote = "1.2.3.4:443"
 
[[endpoints]]
listen = "0.0.0.0:6000"
remote = "5.6.7.8:443"
 
# 常用配置
[network]
use_udp = true
zero_copy = true
 
[[endpoints]]
listen = "0.0.0.0:5000"
remote = "1.2.3.4:443"
 
[[endpoints]]
listen = "0.0.0.0:6000"
remote = "5.6.7.8:443"
 
# 完整配置
[dns]
mode = "ipv4_only"
protocol = "tcp_and_udp"
nameservers = ["1.1.1.1:53", "1.0.0.1:53"]
min_ttl = 600
max_ttl = 3600
cache_size = 256
 
[network]
use_udp = true
zero_copy = true
fast_open = true
tcp_timeout = 300
udp_timeout = 30
send_proxy = false
send_proxy_version = 2
accept_proxy = false
accept_proxy_timeout = 5
 
[[endpoints]]
listen = "0.0.0.0:5000"
remote = "1.2.3.4:443"
 
[[endpoints]]
listen = "0.0.0.0:6000"
remote = "5.6.7.8:443"
```

运行命令 ```systemctl enable realm && systemctl start realm```启动realm
