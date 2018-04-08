# 使用libp2p的聊天室app

这个程序演示了一个简单的p2p聊天应用程序。 它可以在两个peer之间工作
1. 两者都有专用IP地址（相同的网络）。
2. 至少有一个公共IP地址。

假设'A'和'B'在不同的网络上，主机'A'可能有或没有公共IP地址，但主机'B'有一个。

用法：在主机'B'上运行`./chat -sp <SOURCE_PORT>`，其中<SOURCE_PORT>可以是任何端口号。 
然后在节点'A'上运行`./chat -d <MULTIADDR_B>` [`<MULTIADDR_B>`是主机'B'的多地址，可以从主机'B'控制台获得]。

## 构建

要构建该示例，首先在根目录中运行make deps。

```
> make deps
> go build ./examples/chat
```

## 用法

在节点'B'

```
> ./chat -sp 3001
Run ./chat -d /ip4/127.0.0.1/tcp/3001/ipfs/QmdXGaeGiVA745XorV1jr11RHxB9z4fqykm6xCUPX1aTJo

2018/02/27 01:21:32 Got a new stream!
> hi (received messages in green colour)
> hello (sent messages in white colour)
> no
```

在节点'A'上。 如果节点'B'有一个，则将127.0.0.1替换为<PUBLIC_IP>。

```
> ./chat -d /ip4/127.0.0.1/tcp/3001/ipfs/QmdXGaeGiVA745XorV1jr11RHxB9z4fqykm6xCUPX1aTJo
Run ./chat -d /ip4/127.0.0.1/tcp/3001/ipfs/QmdXGaeGiVA745XorV1jr11RHxB9z4fqykm6xCUPX1aTJo

该节点的多地址：
/ip4/0.0.0.0/tcp/0/ipfs/QmWVx9NwsgaVWMRHNCpesq1WQAw2T3JurjGDNeVNWifPS7
> hi
> hello
```

**注意：默认情况下启用调试模式，每次执行时调试模式将始终生成相同的节点标识（在每个节点上）。 在运行可执行文件时，使用`--debug false`标志禁用调试。**

## Authors 作者
1. Abhishek Upperwal