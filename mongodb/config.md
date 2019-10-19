### 让外部客户端可以连接

- 防火墙打开 mongodb 的端口 27017
- net: bindIp: 0.0.0.0 一开始默认为 127.0.0.1

```
net:
  port: 27017
  bindIp: 0.0.0.0
```

### mongod 开启 auth
- ip不限制也不开启auth... 就是sb吧.

```
security:
  authorization: "enabled"
```

### 开机启动mongo

```
/etc/init.d

MONGO_USER=root
MONGO_GROUP=root

这里记得改成当前登录的用户吧... 不然service mongod start gg...
```
