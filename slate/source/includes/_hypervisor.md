# Hypervisor - 宿主机


## Get usage (P0)

```http
GET /hypervisor/usages HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "usages": {
        "instances": 10,
        "memory_used_mb": 20480,
        "memory_total_mb": 50498,
        "cpu_used": 13,
        "cpu_total": 26
    }
}
```

获取宿主机资源使用情况

`GET http://vpe.cds.com/hypervisor/usages`

### Response Body

参数    |  解释
--------|----------
instances    | 当前已经创建的虚拟机个数
memory_used_mb | 当前已经分配给虚拟机使用的内存，单位 MB
memory_total_mb| 总共可以分配给虚拟机使用的内存，单位 MB
cpu_used | 当前已经分配给虚拟机使用的 CPU 个数
cpu_total| 总共可以分配给虚拟机使用的 CPU 个数


## Get metrics (P1)

```http
GET /hypervisor/metrics HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "metrics": {
        "duration": "today",
        "cpu": {
            "unit": "%",
            "datas": {
                "2016-07-10 17:45": 0,
                "2016-07-10 17:50": 0,
                "2016-07-10 17:55": 0,
                "2016-07-10 18:00": 0,
                "2016-07-10 18:05": 0,
                "2016-07-10 18:10": 0,
                "2016-07-10 18:15": 0,
                "2016-07-10 18:20": 0,
                "2016-07-10 18:25": 0,
                "2016-07-10 18:30": 0
            }
        },
        "memory": {
            "unit": "MB",
            "datas": {
                "2016-07-10 17:45": 1000,
                "2016-07-10 17:50": 1000,
                "2016-07-10 17:55": 1000,
                "2016-07-10 18:00": 1000,
                "2016-07-10 18:05": 1200,
                "2016-07-10 18:10": 1200,
                "2016-07-10 18:15": 1200,
                "2016-07-10 18:20": 1200,
                "2016-07-10 18:25": 1200,
                "2016-07-10 18:30": 1200
            }
        },
        "network_in": {
            "unit": "",
            "datas": {
                "2016-07-10 17:45": 1000,
                "2016-07-10 17:50": 1000,
                "2016-07-10 17:55": 1000,
                "2016-07-10 18:00": 1000,
                "2016-07-10 18:05": 1200,
                "2016-07-10 18:10": 1200,
                "2016-07-10 18:15": 1200,
                "2016-07-10 18:20": 1200,
                "2016-07-10 18:25": 1200,
                "2016-07-10 18:30": 1200
            }
        },
        "network_out": {
            "unit": "",
            "datas": {
                "2016-07-10 17:45": 1000,
                "2016-07-10 17:50": 1000,
                "2016-07-10 17:55": 1000,
                "2016-07-10 18:00": 1000,
                "2016-07-10 18:05": 1200,
                "2016-07-10 18:10": 1200,
                "2016-07-10 18:15": 1200,
                "2016-07-10 18:20": 1200,
                "2016-07-10 18:25": 1200,
                "2016-07-10 18:30": 1200
            }
        }
    }
}
```


获取宿主机监控数据，CPU，内存，磁盘，网络

`GET http://vpe.cds.com/hypervisor/metrics?q=`

### Request Parameter


q 参数表示监控数据的时间跨度，可以是如下值，默认为 today。

请求参数|解释
--------|------
today   | 今天
yesterday | 昨天
thisweek | 这周
lastweek | 上周
thismonth | 这个月
lastmonth | 上个月


## Get maximun CPU and Memory (P0)

```http
GET /hypervisor/quota HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "quota": {
        "cpu_max": 16,
        "memory_max_mb": 10240
    }
}
```

`GET http://vpe.cds.com/hypervisor/quota`

### Response Body

参数    |  解释
--------|----------
cpu_max    | 最大可以使用的 cpu 个数
memory_max_mb| 最大可以使用的内存容量，单位 MB

## Update maximum CPU or Memory (P0)

```http
PUT /hypervisor/quota HTTP/1.1
Accept: application/json

{
    "quota": {
        "cpu_max": 16,
        "memory_max_mb": 10240
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "quota": {
        "cpu_max": 16,
        "memory_max_mb": 10240
    }
}
```

修改 CPU 或者内存的使用限制
`PUT http://vpe.cds.com/hypervisor/quota`

<aside class="info">
可以只修改 CPU 或者只修改内存限制，也可以同时修改两个限制。
</aside>

### Request Body

参数    | 是否必须 |  解释
--------|----------|----------
cpu_max | 否 | 最大可以使用的 cpu 个数
memory_max_mb| 否 | 最大可以使用的内存容量，单位 MB

### Response Body

参数    |  解释
--------|----------
cpu_max    | 最大可以使用的 cpu 个数
memory_max_mb| 最大可以使用的内存容量，单位 MB

## Get network configuration (P0)

```http
GET /hypervisor/network HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "network": {
        "bridge": "br100",
        "bridge_interface": "eth0"
    }
}
```

`GET http://vpe.cds.com/hypervisor/network`

### Response Body

参数    |  解释
--------|----------
bridge    | 虚拟机使用的网桥名称，默认是 br100
bridge_interface| 网桥绑定的网卡名，是 eth0，或者 bond0


## Update network configuration (P0)

```http
PUT /hypervisor/network HTTP/1.1

{
    "network": {
        "bridge": "br100",
        "bridge_interface": "eth0"
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "network": {
        "bridge": "br100",
        "bridge_interface": "eth0"
    }
}
```

`PUT http://vpe.cds.com/hypervisor/network`
<aside class="warning">
如果已有虚拟机正在运行，修改网络配置会导致虚拟机网络中断，请谨慎修改。
</aside>

### Request Body

参数    | 是否必须 | 解释
--------|-------|--------
bridge    | 否 |  虚拟机使用的网桥名称，默认是 br100
bridge_interface| 否 | 网桥绑定的网卡名，是 eth0，或者 bond0

## Get image location (P0)

```http
GET /hypervisor/image-pool HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "image-pool": {
        "path": "/home/store/1/vpe/images",
        "max_gb": 1000,
        "used_gb": 0
    }
}
```

获取镜像存放路径配置信息

`GET http://vpe.cds.com/hypervisor/image-pool`

### Response Body

参数    |  解释
--------|----------
path    | 镜像存放的路径，路径必须是系统存在的路径
max_gb  | 镜像最多可以使用的容量


## Update image location (P0)

```http
PUT /hypervisor/image-pool HTTP/1.1

{
    "image-pool": {
        "path": "/home/store/1/vpe/images",
        "max_gb": 1000
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "image-pool": {
        "path": "/home/store/1/vpe/images",
        "max_gb": "1000"
    }
}
```

`PUT http://vpe.cds.com/hypervisor/image-pool`

### Request Body

参数    | 是否必须 | 解释
--------|-------|--------
path    | 否 |  镜像存放的路径，路径必须是系统存在的路径
max_gb  | 否 |  镜像最多可以使用的容量


## List volume pools (P0)

```http
GET /hypervisor/pools HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "pools": [
        {
            "name": "pool1",
            "uuid": "19636f21-dc97-4cde-af55-fd6459342516",
            "path": "/home/store/1/vpe/pool1",
            "max_gb": 30,
            "used_gb": 20,
            "created_at": "2016-02-34 11:22:11"
        },
        {
            "name": "pool2",
            "uuid": "0b2254d3-a306-4140-8c9a-40bceadad234",
            "path": "/home/store/1/vpe/pool2",
            "max_gb": 50,
            "used_gb": 10,
            "created_at": "2016-02-34 11:22:11"
        }
    ]
}
```

获取所有存储路径

`GET http://vpe.cds.com/hypervisor/pools`

### Response Body

参数    |  解释
--------|----------
name   | 存储路径的名称，方便创建虚拟机时选择
uuid   | 存储路径的 uuid
path   | 存储路径的真实路径
max_gb | 存储路径最多可以使用的容量
used_gb| 存储路径已经使用的容量
created_at| 存储路径的创建时间

## Create a volume pool (P0)

```http
POST /hypervisor/pools HTTP/1.1

{
    "pool": {
        "name": "pool2",
        "path": "/home/store/1/vpe/pool2",
        "max_gb": 50
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "pool": {
        "name": "pool1",
        "uuid": "19636f21-dc97-4cde-af55-fd6459342516",
        "path": "/home/store/1/vpe/pool1",
        "max_gb": 30,
        "used_gb": 20,
        "created_at": "2016-02-34 11:22:11"
    }
}
```

`POST http://vpe.cds.com/hypervisor/pools`

## Update a volume pool (P0)

```http
PUT /hypervisor/pools/{uuid} HTTP/1.1

{
    "pool": {
        "name": "pool2",
        "max_gb": 50
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "pool": {
        "name": "pool1",
        "uuid": "19636f21-dc97-4cde-af55-fd6459342516",
        "path": "/home/store/1/vpe/pool1",
        "max_gb": 30,
        "used_gb": 20,
        "created_at": "2016-02-34 11:22:11"
    }
}
```

`PUT http://vpe.cds.com/hypervisor/pools/{id}`

<aside class="info">
路径不能修改，名称和容量可以修改。
容量限制可以修改，缩小不能小于当前已经使用的容量。
</aside>

## Delete a volume pool (P0)

```http
DELETE /hypervisor/pools/{uuid} HTTP/1.1
Content-Type: application/json

{}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "pool": {
        "uuid": "19636f21-dc97-4cde-af55-fd6459342516"
    }
}
```

`DELETE http://vpe.cds.com/hypervisor/pools/{id}`
<aside class="warning">
只有空闲的路径可以被删除，已经在使用的无法删除。
</aside>
