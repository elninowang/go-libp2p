
＃使用libp2p的HTTP代理服务

这个例子展示了如何用libp2p创建一个简单的HTTP代理服务：

```
                                                                                                    XXX
                                                                                                   XX  XXXXXX
                                                                                                  X         XX
                                                                                        XXXXXXX  XX          XX XXXXXXXXXX
                  +----------------+                +-----------------+              XXX      XXX            XXX        XXX
 HTTP Request     |                |                |                 |             XX                                    XX
+----------------->                | libp2p stream  |                 |  HTTP       X                                      X
                  |  Local peer    <---------------->  Remote peer    <------------->     HTTP SERVER - THE INTERNET      XX
<-----------------+                |                |                 | Req & Resp   XX                                   X
  HTTP Response   |  libp2p host   |                |  libp2p host    |               XXXX XXXX XXXXXXXXXXXXXXXXXXXX   XXXX
                  +----------------+                +-----------------+                                            XXXXX
```

为了代理一个HTTP请求，我们创建一个本地Peer，它监听`localhost:9900`。 对该地址执行的HTTP请求通过libp2p流传输到远程Peer，远程Peer然后执行HTTP请求并将响应发送回本地Peer，该Peer将其中继给用户。

请注意，这是一种非常简单的代理方法，不会执行任何标头管理，也不支持HTTPS。 `proxy.go`代码被彻底的推崇，详细说明了每一步中发生的事情。

## 构建

从`go-libp2p`基础文件夹：

```
> make deps
> go build ./examples/http-proxy
```

## 用法

首先按如下方式运行"远程"peer。 它将打印本地Peer地址。 如果您想在单独的机器上运行此操作，请相应地更换IP：

```sh
> ./http-proxy
Proxy server is ready
libp2p-peer addresses:
/ip4/127.0.0.1/tcp/12000/ipfs/QmddTrQXhA9AkCpXPTkcY7e22NK73TwkUms3a44DhTKJTD
```

运行本地Peer，表明它需要将http请求转发给远程peer，如下所示：

```
> ./http-proxy -d /ip4/127.0.0.1/tcp/12000/ipfs/QmddTrQXhA9AkCpXPTkcY7e22NK73TwkUms3a44DhTKJTD
Proxy server is ready
libp2p-peer addresses:
/ip4/127.0.0.1/tcp/12001/ipfs/Qmaa2AYTha1UqcFVX97p9R1UP7vbzDLY7bqWsZw1135QvN
proxy listening on  127.0.0.1:9900
```

如您所见，代理打印监听地址 `127.0.0.1:9900`。 您现在可以将此地址用作代理，例如`curl`：

```
> curl -x "127.0.0.1:9900" "http://ipfs.io/ipfs/QmfUX75pGRBRDnjeoMkQzuQczuCup2aYbeLxz5NzeSu9G6"
it works!
```
