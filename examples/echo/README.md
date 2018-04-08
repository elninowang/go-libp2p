# 使用libp2p回应客户机/服务器

这是一个快速演示如何使用`go-libp2p`堆栈的例子，包括 Host/Basichost，Network/Swarm，Streams，Peerstores和Multiaddresses。

这个例子可以在监听模式或拨号模式下启动。

在监听模式下，它将坐等 `/echo/1.0.0` 协议的传入连接。 每当它接收到流时，它都会在流上写入消息 `"Hello, world!"`并关闭它。

在拨号模式下，节点将启动，连接到给定地址，打开到目标节点的流，并读取协议 `/echo/1.0.0`上的消息。

## 构建

从`go-libp2p`基础文件夹：

```
> make deps
> go build ./examples/echo
```

## 用法

```
> ./echo -secio -l 10000
2017/03/15 14:11:32 I am /ip4/127.0.0.1/tcp/10000/ipfs/QmYo41GybvrXk8y8Xnm1P7pfA4YEXCpfnLyzgRPnNbG35e
2017/03/15 14:11:32 Now run "./echo -l 10001 -d /ip4/127.0.0.1/tcp/10000/ipfs/QmYo41GybvrXk8y8Xnm1P7pfA4YEXCpfnLyzgRPnNbG35e -secio" on a different terminal
2017/03/15 14:11:32 listening for connections
```

侦听器libp2p主机将打印它的`Multiaddress`，它指示如何到达(ip4+tcp)及其随机生成的ID(`QmYo41Gyb...`)

现在，启动另一个与监听器交谈的节点：

```
> ./echo -secio -l 10001 -d /ip4/127.0.0.1/tcp/10000/ipfs/QmYo41GybvrXk8y8Xnm1P7pfA4YEXCpfnLyzgRPnNbG35e
```

新节点向侦听器发送消息`"Hello, world!"`，这个消息会依次在流上回显并关闭它。 侦听器记录消息，并且发送者记录响应。

## 细节

`makeBasicHost()`函数创建一个 [go-libp2p-basichost](https://godoc.org/github.com/libp2p/go-libp2p/p2p/host/basic) 对象。 
`basichost`对象包装[go-libp2 swarms](https://godoc.org/github.com/libp2p/go-libp2p-swarm#Swarm)并应该优先使用。
[go-libp2p-swarm Network](https://godoc.org/github.com/libp2p/go-libp2p-swarm#Network) 是一个Swarm，且符合[go-libp2p-net Network interface](https://godoc.org/github.com/libp2p/go-libp2p-net#Network)，负责维护流，连接，复用不同协议，处理传入连接等。

为了创建swarm（和一个`basichost`），这个例子需要：

- 一个 [ipfs-procotol ID](https://godoc.org/github.com/libp2p/go-libp2p-peer#ID) ，例如`QmNtX1cvrm2K6mQmMEaMxAuB4rTexhd87vpYVot4sEZzxc`。该示例在每次运行时自动生成密钥对，并使用从公钥中提取的ID(公钥的哈希)。使用`-secio`时，它使用密钥对来加密通信（否则，它会使连接未加密）.
- A [Multiaddress](https://godoc.org/github.com/multiformats/go-multiaddr), which indicates how to reach this peer. There can be several of them (using different protocols or locations for example). Example: `/ip4/127.0.0.1/tcp/1234`.
- 一个 [Multiaddress](https://godoc.org/github.com/multiformats/go-multiaddr)，表明如何连接到这个peer。可以有几个(例如不同的协议或不同位置)。例如：`/ip4/127.0.0.1/tcp/1234`.
- 一个 [go-libp2p-peerstore](https://godoc.org/github.com/libp2p/go-libp2p-peerstore)，用作地址簿，将节点ID与多地址相匹配，通过它们可以接触。当手动打开一个连接时（使用 [`Connect()`](https://godoc.org/github.com/libp2p/go-libp2p/p2p/host/basic#BasicHost.Connect)，这个peerstore会自动填充。或者，我们可以手动[`AddAddr()`](https://godoc.org/github.com/libp2p/go-libp2p-peerstore#AddrManager.AddAddr) ，如示例中所示。

一个`basichost`现在可以使用 [NewStream](https://godoc.org/github.com/libp2p/go-libp2p/p2p/host/basic#BasicHost.NewStream) 打开流（到对等点之间的双向通道） 并使用它们来发送和接收标有`Protocol.ID`（一个字符串）的数据。 主机还可以侦听, 为进来传入连接，这个连接上使用了
`Protocol` [`SetStreamHandle()`](https://godoc.org/github.com/libp2p/go-libp2p/p2p/host/basic#BasicHost.SetStreamHandler)。

这个例子利用所有这些来使用协议`/echo/1.0.0`（可以是其他任何东西）来实现监听者和发送者之间的通信。
