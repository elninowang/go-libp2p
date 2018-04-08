

# Protocol Multiplexing using multicodecs with libp2p

# 使用libp2p多代码的协议复用


本示例说明如何使用多代码（即json）在使用LibP2P流的LibP2P主机之间编码和传输信息。

Multicodecs提供了一个通用接口，如果需要的话，可以很容易地交换编解码器实现。

这个例子期望你已经熟悉了 [echo example](https://github.com/libp2p/go-libp2p/tree/master/examples/echo)。

## 构建

From `go-libp2p` base folder:

```
> make deps-protocol-muxing
> go build -o multicodecs ./examples/protocol-multiplexing-with-multicodecs
```

## 用法

```
> ./multicodecs

```

## 细节

该示例创建两个LibP2P主机。 Host1向Host2打开一个流。 Host2有一个`StreamHandler`来处理输入流。 这在`echo`例子中有所介绍。

两台主机都可以模拟对话。 但不是在流上发送原始消息，会话中的每条消息都编码在一个`json`对象下（使用`json`多重代码）。 例如：

```
{
  "Msg": "This is the message",
  "Index": 3,
  "HangUp": false
}
```

当HangUp字段为`true`时，该流持续到其中一方关闭它。
