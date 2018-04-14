# http模块 #
python中的http/https请求使用urllib库，使用urllib的request模块的发送get和post请求。

## get请求 ##
请求网页地址并返回网页html内容，示例如下：
```
from urllib import request


def getHtml(url):
    with request.urlopen(url) as r:
        data = r.read()
        return data.decode("utf-8")


print(getHtml("http://vipstone.cnblogs.com"))
```
对返回的数据进行编码处理data.decode("utf-8")即可。

## post请求 ##
post请求并传递参数，对参数进行encode处理，示例如下：
```
from urllib import request, parse


params = parse.urlencode([("name", "老王"), ("pwd", "123456")])
req = request.Request("http://127.0.0.1:8360/video/login")
req.add_header("User-Agent", "Mozilla/6.0 (iPhone; CPU iPhone OS 8_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/8.0 Mobile/10A5376e Safari/8536.25")

with request.urlopen(req, data=params.encode("utf-8")) as r:
    data = r.read()
    print(data.decode("utf-8"))
```
如上所示，需要使用urllib的parse对参数进行编码处理，也可以给http头添加内容。