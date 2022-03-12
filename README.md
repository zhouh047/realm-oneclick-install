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
installed: /usr/local/etc/realm/config.json
```

### 安装
```
wget --no-check-certificate -O realm.sh https://raw.githubusercontent.com/zhouh047/realm-oneclick-install/main/realm.sh && bash realm.sh -i
```

### 卸载
```
wget --no-check-certificate -O realm.sh https://raw.githubusercontent.com/zhouh047/realm-oneclick-install/main/realm.sh && bash realm.sh -u
```

### 注意
本脚本没有自动配置转发，也没有启动realm。

请编辑```/usr/local/etc/realm/config.json```，添加转发配置。
配置示例
```
配置文件支持端口段，当转发端口的数量大于本地地址时，都会默认使用第一个传入的地址。这样实现了一个地址上的多端口转发多ip或单ip上的多端口。
{
    "listening_addresses": ["0.0.0.0"],
    "listening_ports": ["30000-30001"],
    "remote_addresses": ["10.211.55.5", "10.211.55.6"],
    "remote_ports": ["39515", "53924"]
}
```

运行命令 ```systemctl enable --now realm && systemctl start realm```启动realm

