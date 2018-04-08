# 使用 rpc-style multicodecs, protobufs与libp2p 进行协议复用


本示例说明如何使用multicodecs（即protobufs）在使用LibP2P流的LibP2P主机之间编码和传输信息。
Multicodecs提供了一个通用接口，如果需要的话，可以很容易地交换编解码器实现。
这个例子期望你已经熟悉了[echo example](https://github.com/libp2p/go-libp2p/tree/master/examples/echo)。

## 构建

安装gx: 
```sh
> go get -u github.com/whyrusleeping/gx

```

从根libp2p源代码目录 运行GX:
```sh
>gx install
```

构建libp2p:
```sh
> make deps
> make
```

在`multipro`文件夹下运行

```sh
> go build
```


## 用法

```sh
> ./multipro

```

## 细节

该示例创建了两个支持2种协议的LibP2P主机：ping和echo。

每个协议都由RPC风格的请求和响应组成，每个请求和响应都是一个类型化的protobufs消息（和一个数据对象）。

这是一种不同的模式，然后将整个p2p协议定义为一个包含许多可选字段的protobuf消息（如可以在使用protobufs（如dht）的各种p2p-lib协议中观察到的那样）。

该示例显示如何将收到的异步响应与其请求进行匹配。 处理响应需要访问请求数据时，这非常有用。

这个想法是在每个消息的基础上使用lib-p2p协议复用。

### 特征

1. 2使用类似RPC的请求 - 响应模式完全实现的协议 - Ping和Echo
2. Scaffolding ，用于快速实施新的应用程序级版本化RPC类协议
3. 作者（可能不是消息的发件peer）对传入消息数据的完全身份验证
4. 在protobufs中使用所有协议消息共享字段的基础p2p格式
5. 处理响应时完全访问请求数据。

## 作者
@avive