![xkcptun](https://github.com/liudf0716/xkcptun/blob/master/logo-big.png)

[![Build Status][1]][2]  [![Powered][3]][4]

[1]: https://travis-ci.org/liudf0716/xkcptun.svg?branch=master
[2]: https://travis-ci.org/liudf0716/xkcptun
[3]: https://img.shields.io/badge/KCP-Powered-blue.svg
[4]: https://github.com/skywind3000/kcp

# xkcptun 基于kcp和libevent2库，用c语言实现的kcptun

xkcptun主要应用于LEDE，openwrt中，其原理如图：

<img src="kcptun.png" alt="kcptun" height="300px"/>

### Compile

xkcptun依赖[libevent2](https://github.com/libevent/libevent)和[json-c](https://github.com/json-c/json-c)

安装libevent2和json-c库后

git clone https://github.com/liudf0716/xkcptun.git

cd xkcptun

mkdir build && cd build

cmake ..

make


生成xkcp_client, xkcp_server, xkcp_spy

#### 参考文档

1, [安装libjson c的问题](https://github.com/liudf0716/xkcptun/wiki/%E5%AE%89%E8%A3%85libjson-c%E7%9A%84%E9%97%AE%E9%A2%98)

2, [bbr vs kcp  优化http下载性能对比报告](https://github.com/liudf0716/xkcptun/wiki/bbr-vs-kcp-%E4%BC%98%E5%8C%96http%E4%B8%8B%E8%BD%BD%E6%80%A7%E8%83%BD%E5%AF%B9%E6%AF%94%E6%8A%A5%E5%91%8A)

### OpenWrt
编译及安装请参考 [openwrt-xkcptun](https://github.com/gigibox/openwrt-xkcptun)

### QuickStart

为方便理解和使用，我们将使用场景放在同一台pc上，pc使用ubuntu系统，我们通过xkcptun来访问本机的http server

假设pc的 eth0 ip 为 192.168.199.18， http server的监听端口为80端口，xkcptun的server和client配置分别如下：

server.json 如下：
```
{
  "localinterface": "eth0",
  "localport": 9089,
  "remoteaddr": "192.168.199.18",
  "remoteport": 80,
  "key": "14789632a",
  "crypt": "none",
  "mode": "fast3",
  "mtu": 1350,
  "sndwnd": 1024,
  "rcvwnd": 1024,
  "datashard": 10,
  "parityshard": 3,
  "dscp": 0,
  "nocomp": true,
  "acknodelay": false,
  "nodelay": 0,
  "interval": 20,
  "resend": 2,
  "nc": 1,
  "sockbuf": 4194304,
  "keepalive": 10
}
```

client.json如下：
```
{
  "localinterface": "eth0",
  "localport": 9088,
  "remoteaddr": "192.168.199.18",
  "remoteport": 9089,
  "key": "14789632a",
  "crypt": "none",
  "mode": "fast3",
  "mtu": 1350,
  "sndwnd": 1024,
  "rcvwnd": 1024,
  "datashard": 10,
  "parityshard": 3,
  "dscp": 0,
  "nocomp": true,
  "acknodelay": false,
  "nodelay": 0,
  "interval": 20,
  "resend": 2,
  "nc": 1,
  "sockbuf": 4194304,
  "keepalive": 10
}
```

分别运行：

xkcp_server -c server.json -f -d 7

xkcp_client -c client.json -f -d 7


curl http://192.168.199.18:9088

其执行效果与curl http://192.168.199.18 等同


xkcp_spy -h 192.168.199.18 -s -t status

查看服务器端的情况

xkcp_spy -h 192.168.199.18 -c -t status

查看客户端的情况

### How to contributor(给本项目做贡献)


欢迎大家给本项目提供意见和贡献，提供意见的方法可以在本项目的[Issues](https://github.com/liudf0716/xkcptun/issues/new)提，更加欢迎给项目提PULL REQUEST，具体提交PR的方法请参考[CONTRIBUTING](https://github.com/liudf0716/xkcptun/blob/master/CONTRIBUTING.md)


### Contact me 

QQ群 ： [331230369](https://jq.qq.com/?_wv=1027&k=47QGEhL)


## Please support us, please star our project
