代码阅读工具；Sourcegraph

## Caddy标准模块

[caddy/modules/standard](https://sourcegraph.com/github.com/caddyserver/caddy/-/blob/modules/standard/imports.go)中初始化了caddy内建的标准模块
```go
package standard

import (
	// standard Caddy modules
	_ "github.com/caddyserver/caddy/v2/caddyconfig/caddyfile"
	_ "github.com/caddyserver/caddy/v2/modules/caddyhttp/standard"
	_ "github.com/caddyserver/caddy/v2/modules/caddypki"
	_ "github.com/caddyserver/caddy/v2/modules/caddypki/acmeserver"
	_ "github.com/caddyserver/caddy/v2/modules/caddytls"
	_ "github.com/caddyserver/caddy/v2/modules/caddytls/distributedstek"
	_ "github.com/caddyserver/caddy/v2/modules/caddytls/standardstek"
	_ "github.com/caddyserver/caddy/v2/modules/filestorage"
	_ "github.com/caddyserver/caddy/v2/modules/logging"
	_ "github.com/caddyserver/caddy/v2/modules/metrics"
)
```

从中可以看出自建模块有：

+ logging: 日志的格式化、过滤、输出等功能
+ caddyfile: caddy配置的解析、加载、格式化等功能
+ filestorage:  certmagic.FileStorage的简单封装
+ metrics: 
+ caddypki:
    + caddypki/acmeserver :Automated Certificate Management Environment  Server（自动证书管理环境服务器）
+ caddytls
    + /caddytls/distributedstek
    + caddytls/standardstek
+ caddyhttp （非常核心的一个模块）:
	+ caddyauth ： 处理HTTP-AUTH相关
	+ encode：编码相关
        + encode/gzip： 对content进行gzip压缩处理
        + encode/zstd:  对content进行zstd研所处理
	+ fileserver: 静态文件服务处理
	+ headers: HTTP Headers 处理
	+ map: 是将源占位符映射到目标占位符的中间件
	+ push: 请求体处理中间件
	+ requestbody: 请求体处理中间件
	+ reverseproxy： 高度可配置的反向代理
	+ reverseproxy/fastcgi： 
	+ rewrite： rewrite HTTP请求的中间件
	+ templates： 模板处理中间件。将响应体按照go-template文件继续宁render渲染处理（就像直接将markdown渲染成html，而不是响应原始的Markdown文本）
)



## Caddy 配置相关

主要在 [caddy/caddyconfig](https://sourcegraph.com/github.com/caddyserver/caddy/-/tree/caddyconfig)

caddyconfig作为caddy的一个moudle存在，注册使用

+ 配置加载器:[caddy/caddyconfig/load.go]
+ 配置适配器:[caddy/caddyconfig/configadpters.go]
+ 配置实现（配置格式化）
    + caddyfile
    + httpcaddyfile

## 

