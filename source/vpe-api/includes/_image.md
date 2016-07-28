# Images - 镜像

## List images (P0)

```http
GET /images HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "images": [
        {
            "uuid": "bc9b3011-b56a-4340-b787-a77021cf57b8",
            "location": "/home/vpe/images/cirros.qcow2",
            "size": 10,
            "created_at": "2016-02-33 11:22:33",
            "instance_count": 3
        },
        {
            "uuid": "d838fac2-d601-4210-96dd-073968731433",
            "location": "/home/vpe/images/images.qcow2",
            "size": 40,
            "created_at": "2016-02-33 11:22:33",
            "instance_count": 0
        }
    ]
}
```

`GET http://vpe.cds.com/images`

### Response Body
属性   |  解释
-------|-----------
uuid   |镜像的 uuid
location | 镜像的路径名称
size   | 镜像大小,单位 MB
created_at| 镜像的创建时间
instance_count| 使用该镜像的虚拟机个数

