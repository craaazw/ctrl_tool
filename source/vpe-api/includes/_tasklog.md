# Tasklog - 操作日志

## List tasklogs (P0)

```http
GET /tasklogs HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "tasklogs": [
        {
            "action": "create instance",
            "resource": "instance1",
            "status": "success",
            "created_at": "2016-02-33 11:22:33",
            "duration": 2
        },
        {
            "action": "stop instance",
            "resource": "instance1",
            "status": "success",
            "created_at": "2016-02-33 11:22:33",
            "duration": 3
        }
    ]
}
```

获取操作记录
`GET http://vpe.cds.com/tasklogs?start=2016-02-02 11:22:11&end`

### Query Parameters

参数 | 说明
-----|-------------------------------
start| 开始时间：2016-02-02 11:22:11, 如果没有指定则开始时间为一小时前
end  | 结束时间：2016-03-01 12:11:22, 如果没有指定则为当前时间


### Response Body
属性   |  解释
-------|-----------
action   |操作名。如：create instance
resource | 被操作的对象名称
status  | 操作结果: success，failed
created_at| 操作开始时间
duration | 操作用时，单位秒
