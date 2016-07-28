# Errors - 错误约定

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
    "error": {
        "code": 400,
        "message": "instance 'vm1' already existed."
    }
}
```

VPE 使用如下错误约定。


Error Code | Meaning
---------- | -------
400 | 请求格式非法或者请求的内容不符合要求
401 | 认证失败，用户名或者密码不正确
403 | 权限不足，没有权限访问这个接口
404 | 找不到对应的接口，或者资源不存在
429 | 超过了访问频率限制
500 | 内部错误，服务端异常
503 | 服务不可用，服务正在维护中暂时无法使用
