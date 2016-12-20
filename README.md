# caas

caas还在原型设计状态，不可用。

下面几个维度可能决定最终配置文件的差异。

- 客户端版本
- 服务器版本
- 城市
- 设备
- token

## Objective-C

```Objective-C
/**
 * 第二个参数是默认值
 */
(void *)get(NSString *key, ...);
(int)getInt(NSString *key, ...);
(float)getFloat(NSString *key, ...);
(NSString)getString(NSString *key, ...);

get("system.site.name")
// will print http://example.com

get("ui.homepage.font_size", 12);
// 如果不存在，将返回12

get("ui.homepage.banner[0].image_url")
// [index] 

get("ui.homepage.banner[last]") 

get("ui.homepage.banner[-2]")

get("current.sitename", "shmg");

get("site.${current.sitename}.articles)

get("sites[@site.name=SHMG]", "shmg");
// current.sitename 作为变量访问指定的site的属性名

```

## 本地配置文件作为数据源

```
{
  current: {
  	sitename: "shmg"
  },
  sites: [
    {
      "name": "SHMG",
      "articles": [
      ]
    },
    {
      "name": "SHMG Incubator"
    }
  ]
}
```

## HTTP API - GET /

version 可以做增量更新，增量更新只会更新差异部分的数据。因为version的缘故，所有的数据修改都会存有历史记录。这些历史在增量更新的时候可以合并。

```
GET / ?module=system.site&version=10 HTTP 1.1
HOST: host

HTTP/1.1 200 OK
Content-Type: application/json

{
}
```

## Request parameter

- module 类型 string，如system可以得到system这个模块的所有数据
- version 纯数字的数据版本号
- client_version string 客户端版本号，比如iOS 版本是0.0.9，android版本是0.0.1。
- server_version string 表示当前配置的模型的版本号
- city int
- device string

## HTTP API - POST /

配置键值

```
POST /?module=system HTTP 1.1
HOST: host

HTTP/1.1 200 OK
Content-Type: text/html

keypath=system.site.name&value=SHMG
```

追加到数组的尾部

```
keypath=system.site.name[]&value=SHMG
```

设置Object

```
keypath=system.site.image&value={
  "url": "",
  "context-type": "image/jpeg"
}
```
