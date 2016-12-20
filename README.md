# caas

不同的客户端版本。
不同的城市。
不同的设备。
指定的token。

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
// current.sitename 作为变量访问指定的site的属性名
```

## HTTP API

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
- version 数字

version 可以做增量更新，只会更新到差异部分的数据。
