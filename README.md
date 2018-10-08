# ant_tsl_golang_modules

## Source
[golang wiki: Modules](https://github.com/golang/go/wiki/Modules/1adc543ca9590fed6556fad4795b4fc479158d1b)
并不是完全地翻译.

## Go 1.11 Modules
Go 1.11 包含了对[版本化模块](https://golang.org/design/24301-versioned-go)的初步支持, 也就是 Modules. Modules 被作为一个实验性质的可选择加入的特性放入到 Go 1.11 中, 用以整合反馈, 并为 Go 1.1的特性做定案. 未来的发行版本即使在细节上会有变化, 依然会支持使用 Go 1.11 或者 `vgo` 定义的模块

一句话, Modules 是 Go 的包管理工具, 就像 Maven, Gradle.

## 使用 Modules
### Install
* [安装最新的 Go 1.11 发行版](https://golang.org/dl/)
* [从源码主分支上安装 Go 工具链](https://golang.org/doc/install/source)

直接下载安装包吧, 一步搞定, 比较省心.

### Activate
两种方式来激活`module`支持
* 设置环境变量`GO111MODULE=on`, 按照之前的习惯去使用`go`命令
* 在特定的目录下使用`go`命令, 该目录不在`$GOPATH/src`目录树下, 该目录下或者该目录的任何父目录下包含有效的`go.mod`文件; 且, 不要设置环境变量`GO111MODULE`或者明确设置环境变量`GO111MODULE=on`.

### 定义一个模块

### 升级或者降级依赖

### 发布模块

## 概念
### Mock Start
在说具体的概念前, 我们需要有个从零开始的假栗子

在你的环境变量 GOPATH 路径外 创建一个目录: 
```
# 可以使用 go env GOPATH 查看 GOPATH
$ mkdir -p /tmp/scratchpad/hello
$ cd /tmp/scratchpad/hello
```
初始化一个模块(`module`):
```
$ go mod init github.com/you/hello

go: creating new go.mod: module github.com/you/hello
```
写代码:
```
$ cat <<EOF > hello.go
package main

import (
    "fmt"
    "rsc.io/quote"
)

func main() {
    fmt.Println(quote.Hello())
}
EOF
```
构建并运行:
```
$ go build 
$ ./hello

Hello, world.
```
注意`go.mod`已经包含了你的依赖的明确版本
```
$ cat go.mod

module github.com/you/hello

require rsc.io/quote v1.5.2
```

### Modules 模块
`Module`: 模块是一组有关联的包(`Go package`), 这些包被当做一个单一的单元来版本化.   

### go.mod
