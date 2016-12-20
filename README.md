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

## HTTP API

## 查询配置文件
```
GET /?module=system HTTP 1.1
HOST: host

HTTP/1.1 200 OK
Content-Type: application/json

{
  "name": "SHMG"
}
```

## 请求参数

请求参数是 QueryString

- module string 如system可以得到system这个模块的所有数据

## 修改配置文件

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
