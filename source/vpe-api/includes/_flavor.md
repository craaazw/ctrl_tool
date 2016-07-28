# Flavors - 配方

## List flavors (P0)

```http
GET /flavors HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "flavors": [
        {
            "uuid": "bc9b3011-b56a-4340-b787-a77021cf57b8",
            "name": "m1.micro",
            "vcpus": 1,
            "memory_mb": 1024,
            "disk_gb": 10,
            "nics": 2
        },
        {
            "uuid": "ef8a1fa5-9671-46fc-bdf2-43c49ba0b8bc",
            "name": "m1.large",
            "vcpus": 3,
            "memory_mb": 2048,
            "disk_gb": 10,
            "nics": 1
        }
    ]
}
```

`GET http://vpe.cds.com/flavors`

### Response Body

参数    |  解释
--------|----------
uuid    | 配方的uuid
name    | 配方的名称
vcpus | 使用该配方的虚拟机将被分配多少个 vcpu
memory_mb | 使用该配方的虚拟机将被分配多少 MB 内存
disk_gb  | 使用该配方的虚拟机系统盘将被分配多少 GB 磁盘
nics     | 使用该配方的虚拟机将会被分配多少网卡
