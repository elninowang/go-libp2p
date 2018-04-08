
<h1 align="center">
  <a href="libp2p.io"><img width="250" src="https://github.com/libp2p/libp2p/blob/master/logo/alternates/libp2p-logo-alt-2.png?raw=true" alt="libp2p hex logo" /></a>
</h1>

<h3 align="center">The Go implementation of the libp2p Networking Stack.</h3>

<p align="center">
  <a href="http://ipn.io"><img src="https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square" /></a>
  <a href="http://libp2p.io/"><img src="https://img.shields.io/badge/project-libp2p-blue.svg?style=flat-square" /></a>
  <a href="http://webchat.freenode.net/?channels=%23ipfs"><img src="https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square" /></a>
  <a href="https://waffle.io/libp2p/libp2p"><img src="https://img.shields.io/badge/pm-waffle-blue.svg?style=flat-square" /></a>
</p>

<p align="center">
  <a href="https://travis-ci.org/libp2p/go-libp2p"><img src="https://travis-ci.org/libp2p/go-libp2p.svg?branch=master" /></a>
  <!--<a href="https://circleci.com/gh/libp2p/go-libp2p"><img src="https://circleci.com/gh/libp2p/go-libp2p.svg?style=svg" /></a>-->
  <!--<a href="https://coveralls.io/github/libp2p/go-libp2p?branch=master"><img src="https://coveralls.io/repos/github/libp2p/go-libp2p/badge.svg?branch=master"></a>-->
  <br>
  <a href="https://github.com/RichardLitt/standard-readme"><img src="https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square" /></a>
  <a href="https://godoc.org/github.com/libp2p/go-libp2p"><img src="https://godoc.org/github.com/ipfs/go-libp2p?status.svg" /></a>
  <a href=""><img src="https://img.shields.io/badge/golang-%3E%3D1.8.0-orange.svg?style=flat-square" /></a>
  <br>
</p>

# 项目状态

[![Throughput Graph](https://graphs.waffle.io/libp2p/go-libp2p/throughput.svg)](https://waffle.io/libp2p/go-libp2p/metrics/throughput)

# Table of Contents

- [背景](#background)
- [绑定](#bundles)
- [用法](#usage)
  - [安装](#install)
  - [API](#api)
  - [示例](#examples)
- [开发](#development)
  - [测试](#tests)
  - [包](#packages)
- [帮助我们](#contribute)
- [许可](#license)

## 背景

[libp2p](https://github.com/libp2p/specs)是一个网络栈和模块化的[IPFS项目](https://github.com/ipfs/ipfs)，并分别捆绑为其他工具使用。
> 
libp2p是长期而艰苦的理解追求的产物 - 深入探索互联网的网络堆栈，以及过去丰富的点对点协议。 在过去的15年中构建大规模的点对点系统非常复杂且困难，libp2p是解决这个问题的一种方法。 它是一个“网络协议栈” - 一种协议套件，它可以清楚地分离问题，并使复杂的应用程序只使用他们绝对需要的协议，而不会放弃互操作性和可升级性。 libp2p由IPFS发展而来，但它的构建使许多人可以使用它，适用于许多不同的项目。
>
> 我们将编写一套文档，文章，教程和讲座来解释p2p是什么，它为什么非常有用，以及它如何帮助您现有的和新的项目。 但在此期间，请检查
>
> - [**The libp2p Specification**](https://github.com/libp2p/specs)
> - [**go-libp2p implementation**](https://github.com/libp2p/go-libp2p)
> - [**js-libp2p implementation**](https://github.com/libp2p/js-libp2p)


## 捆绑

目前只有一包`go-libp2p`，这个包。 该软件包由[`go-ipfs`]使用。

## 用法

`go-libp2p` repo是构成Go libp2p的Go模块列表以及其入口点。

### 安装

```bash
> go get -d github.com/libp2p/go-libp2p/...
> cd $GOPATH/src/github.com/libp2p/go-libp2p
> make
> make deps
```

### API

[![GoDoc](https://godoc.org/github.com/ipfs/go-libp2p?status.svg)](https://godoc.org/github.com/libp2p/go-libp2p)

### 示例

示例可以在[examples folder]上找到（示例）。

## 开发

### 依赖

在开发过程中，您需要使用[gx来安装并链接您的依赖项](https://github.com/whyrusleeping/gx#dependencies)，执行以下操作：

```sh
> make deps
```

在提交并推送到Github之前，请确保将依赖项的礼物倒回。 你可以这样做：

```sh
> make publish
```

### 测试

独立测试的运行是通过gx test `<path to test>` 完成

```bash
$ cd $GOPATH/src/github.com/libp2p/go-libp2p
$ make deps
$ gx test ./p2p/<path of module you want to run tests for>
```

### 包

> **WIP**

libp2p当前存在的软件包列表：

| Package            | Version | CI                  |
|--------------------|---------|---------------------|
| **Transports**                                     |
| **Connection Upgrades**                            |
| **Stream Muxers**                                  |
| **Discovery**                                      |
| **Crypto Channels**                                |
| **Peer Routing**                                   |
| **Content Routing**                                |
| **Miscellaneous**                                  |
| **Data Types**                                     |

# 帮助我们 

go-libp2p是[The IPFS Project](https://github.com/ipfs/ipfs)的一部分，并且是MIT许可的开源软件。 我们欢迎大大小小的贡献！ 看看[社区贡献笔记](https://github.com/ipfs/community/blob/master/contributing.md)。 请确保检查[问题](https://github.com/ipfs/go-libp2p/issue)。 在提交问题之前搜关闭的内容，并帮助我们开放。

指南

- 阅读[libp2p规格](https://github.com/libp2p/specs)
- 即使在主存储库上工作，也请提出分支机构+拉取请求
- 在[Issues问题](https://github.com/libp2p/go-libp2p/issues)或freenode上的#ipfs中提出问题或讨论问题。
- 确保你能够做出贡献（请不要出现法律问题 - 我们使用DCO）
- 在推送任何代码之前运行`go fmt`
- 运行`golint`和`go vet` - 有些东西（比如protobuf文件）预计会失败。
- 联系@jbenet和@diasdavid了解如何做出最佳贡献
- 玩的开心！

你现在可以做些事情来帮忙：

 - 浏览以下模块并**检查现有问题**。 这对积极开发中的模块特别有用。 可能需要一些关于IPFS/libp2p的知识，以及背后的infrasture - 例如，您可能需要阅读p2p和更复杂的操作（如复用）才能在技术上提供帮助。
  - **执行代码评论**。
  - **添加测试**。 永远不会有足够的测试。

## 模块化go-libp2p

目前我们正在进行一项工作，即将rep-monolith中的go-libp2p模块化到不同仓库中的几个软件包，这些软件包可以重复用于其他交换自定义libp2p版本的项目。

我们希望保留历史记录，所以我们将使用git-subtree来提取包。 查找以下说明：

```sh
# 1) create the extracted tree (has the directory specified as -P as its root)
> cd go-libp2p/
> git subtree split -P p2p/crypto/secio/ -b libp2p-secio
62b0a5c21574bcbe06c422785cd5feff378ae5bd
# important to delete the tree now, so that outdated imports fail in step 5
> git rm -r p2p/crypto/secio/
> git commit
> cd ../

# 2) make the new repo
> mkdir go-libp2p-secio
> cd go-libp2p-secio/
> git init && git commit --allow-empty

# 3) fetch the extracted tree from the previous repo
> git remote add libp2p ../go-libp2p
> git fetch libp2p
> git reset --hard libp2p/libp2p-secio

# 4) update self import paths
> sed -someflagsidontknow 'go-libp2p/p2p/crypto/secio' 'golibp2p-secio'
> git commit

# 5) create package.json and check all imports are correct
> vim package.json
> gx --verbose install --global
> gx-go rewrite
> go test ./...
> gx-go rewrite --undo
> git commit

# 4) make the package ready
> vim README.md LICENSE
> git commit

# 5) bump the version separately
> vim package.json
> gx publish
> git add package.json .gx/
> git commit -m 'Publish 1.2.3'

# 6) clean up and push
> git remote rm libp2p
> git push origin master
```
