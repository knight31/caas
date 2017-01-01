# caas

Caas 是 configuration as a service 的简称。caas设计的目的是希望可以有一个开箱即用的配置
文件工具集。包含 Objective-C, Java 等客户端的配置文件，也包含服务端应用程序。

目前caas正在创意阶段，没有任何可用的组件。

## 客户端特性

- 从网络查询配置文件
- 本地缓存和缓存更新机制
- 从服务器推送更新

## Objective-C 安装

编辑 Podfile。

> 伪码，忘记Podfile的正确写法了。

```
pod 'imcj/caas'
```

```
$ pod install
```

## Objective-C 使用指南

@songtao046 等待你们完善。

```
// 点符号访问对象，第二个参数是默认值
get("ui.homepage.font_size", 12);

// 可以使用[index]的形式访问数组
get("ui.homepage.banner[0].image_url", "http://example.com/1.jpg")
```

## HTTP API

caas提供一组api接口用于读取和保存配置信息。客户端使用http api接口读取配置，接口返回json格式的数据。

```shell
# 查询配置文件
$ curl http://caas.shmakegroup.cn/
{
    "name": "Caas"
}

# 上传配置文件
$ curl http://caas.shmakegroup.cn/ -X POST -F module=default -F data=@conf.json
```

## 核心团队成员

贡献代码后自行在这个位置插入自己的信息。

- [@CJ](https://github.com/imcj)

## Changelog

## Contributing

## Copyright

Copyright .See [LICENSE](LICENSE) for details.
