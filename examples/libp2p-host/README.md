# libp2p '主机'

对于大多数应用程序来说，主机是您开始所需的基本构建块。 本指南将介绍如何构建和使用简单的主机。

主机是一个管理群体顶部服务的swarm。 它提供了一个干净的接口来连接到给定的远程peer服务。

首先，您需要一个ID和一个地方来存储该ID。 要生成ID，您可以执行以下操作：

```go
import (
	"crypto/rand"

	crypto "github.com/libp2p/go-libp2p-crypto"
	peer "github.com/libp2p/go-libp2p-peer"
	pstore "github.com/libp2p/go-libp2p-peerstore"
)

// Generate an identity keypair using go's cryptographic randomness source
priv, pub, err := crypto.GenerateEd25519Key(rand.Reader)
if err != nil {
	panic(err)
}

// A peers ID is the hash of its public key
pid, err := peer.IDFromPublicKey(pub)
if err != nil {
	panic(err)
}

// We've created the identity, now we need to store it.
// A peerstore holds information about peers, including your own
ps := pstore.NewPeerstore()
ps.AddPrivKey(pid, priv)
ps.AddPubKey(pid, pub)
```

接下来，您至少需要一个您想要监听的地址。 你可以像这样从一个字符串到一个multiaddr：

```go
import ma "github.com/multiformats/go-multiaddr"

...

maddr, err := ma.NewMultiaddr("/ip4/0.0.0.0/tcp/9000")
if err != nil {
	panic(err)
}
```

现在你知道你是谁了，你住在哪里(以一种说话的方式)。 下一步是建立一个'swarm network'来处理你要连接的所有peer。 该swarm处理来自其他peer的传入连接，并处理新的出站连接的协议。

```go
import (
	"context"
	swarm "github.com/libp2p/go-libp2p-swarm"
)

// Make a context to govern the lifespan of the swarm
ctx := context.Background()

// Put all this together
netw, err := swarm.NewNetwork(ctx, []ma.Multiaddr{maddr}, pid, ps, nil)
if err != nil {
	panic(err)
}
```

在这一点上，我们拥有最终构建主机所需的一切。 这个调用是目前为止最简单的一个：

```go
import bhost "github.com/libp2p/go-libp2p/p2p/host/basic"

myhost := bhost.New(netw)
```

这就是它，你有一个libp2p主机，你准备开始做一些很棒的P2P网络！

在将来的指南中，我们将讨论如何使用主机，以不同方式配置它们（提示：有很多种方法来设置它们），以及将这种技术应用到您可能想要构建的各种应用程序的有趣方法。


要将这些代码放在一起，请查看[host.go](host.go)。
