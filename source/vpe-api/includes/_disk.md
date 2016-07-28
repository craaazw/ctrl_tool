# Disks - 磁盘

## List disks (P0)

```http
GET /disks HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "disks": [
        {
            "name": "disk1",
            "uuid": "908234a5-825d-4f76-83cc-4e3e7e83d651",
            "pool": "pool1",
            "pool_uuid": "769ee130-b745-42b9-9ef8-60a937b46f80",
            "status": "active",
            "size": 10,
            "instance": "vm2",
            "instance_uuid": "61d20820-cef7-4a92-bcdb-ab1bd4db6c6b",
            "created_at": "2016-07-15 11:22:33"
        },
        {
            "name": "disk2",
            "uuid": "be9a7f52-2395-48de-ac74-7c102e111092",
            "pool": "pool1",
            "pool_uuid": "769ee130-b745-42b9-9ef8-60a937b46f80",
            "status": "active",
            "size": 10,
            "instance": null,
            "instance_uuid": null,
            "created_at": "2016-07-16 11:22:33"
        }
    ]
}
```

`GET /disks`

### Response Body

参数    |  解释
--------|----------
name    | 磁盘名，长度255字节，英文字母或数字
uuid    | 磁盘的uuid
pool    | 磁盘所属的 pool 名称
pool_uuid | 磁盘所属 pool 的 uuid
status  | 磁盘当前状态：active, available, disabled
size | 磁盘的大小，单位是 GB
instance| 挂载的虚拟机，如果未挂载，则当前字段为 null
instance_uuid| 挂载的虚拟机 uuid，如果未挂载，则当前字段为 null
created_at  | 磁盘的创建时间

## Create disk (P0)

```http
POST /disks HTTP/1.1
Accept: application/json

{
    "disk": {
        "name": "disk1",
        "pool_uuid": "769ee130-b745-42b9-9ef8-60a937b46f80",
        "size": 10
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "disk": {
        "uuid": "908234a5-825d-4f76-83cc-4e3e7e83d651",
        "name": "disk1",
        "pool": "pool1",
        "pool_uuid": "769ee130-b745-42b9-9ef8-60a937b46f80",
        "status": "active",
        "size": 10,
        "instance": null,
        "instance_uuid": null,
        "created_at": "2016-07-15 11:22:33"
    }
}
```

`POST /disks`

### Request Body

参数    |  解释
--------|----------
name | 磁盘的名字
pool_uuid| 磁盘所属的路径 uuid
size | 磁盘的大小，单位是 GB



## Delete disk (P0)

```http
DELETE /disks/{uuid} HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "disk": {
        "uuid": "908234a5-825d-4f76-83cc-4e3e7e83d651"
    }
}
```

`DELETE /disks/{uuid}`
