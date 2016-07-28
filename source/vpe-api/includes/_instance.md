# Instances - 虚拟机

## List instances (P0)

列出所有虚拟机概要信息。

```http
GET /instances?name=en HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instances": [
    {
        "uuid": "22c91117-08de-4894-9aa9-6ef382400985",
        "name": "vm1",
        "image": "centos6.7",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "disk_pool": "pool2",
        "disk_pool_uuid": "w3rwexc-1c39-4bc6-81c1-07e3600faa65",
        "status": "active",
        "task": "creating",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "flavor": "m1.tiny",
        "ha": false,
        "tags": ["private", "production"],
        "created_at": "2016-11-22 10:22:32",
        "disks": [
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol1"
            },
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol2"
            }
        ]
    },
    {
        "uuid": "33c11117-08de-4894-9aa9-6ef382400985",
        "name": "vm3",
        "image": "centos6.7",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "disk_pool": "pool2",
        "disk_pool_uuid": "w3rwexc-1c39-4bc6-81c1-07e3600faa65",
        "status": "active",
        "task": "creating",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "flavor": "m2.large",
        "ha": false,
        "tags": ["private", "production"],
        "created_at": "2016-11-22 10:22:32",
        "disks": []
    },
    ]
}
```


### HTTP Request

`GET http://vpe.cds.com/instances`

### Query Parameters
Parameter | Default | Description
----------|---------|------------
name | - | 根据虚拟机名称进行搜索

### Response Body

参数    |  解释
--------|----------
name   | 虚拟机的名称
uuid   | 虚拟机的 uuid
image  | 虚拟机使用的镜像名称
image_uuid| 虚拟机使用的镜像的 uuid
disk_pool | 虚拟机系统盘使用的存储路径的名称
disk_pool_uuid | 虚拟机系统盘使用的存储路径的 uuid
status | 虚拟机状态信息：active, shutoff
task   | 虚拟机当前正在执行的任务：creating, deleting
flavor | 虚拟机使用的配方名称
flavor_uuid | 虚拟机使用的配方的 uuid
ha | 虚拟机是否是高可用模式。高可用虚拟机保证虚拟机永远是上电状态
tags | 虚拟机标签，标签方便对虚拟机进行分类
created_at| 虚拟机的创建时间
disks | 虚拟机挂载的数据盘列表

## Show instance detail (P0)


```http
GET /instances/22c91117-08de-4894-9aa9-6ef382400985 HTTP/1.1
Accept: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instance": {
        "uuid": "22c91117-08de-4894-9aa9-6ef382400985",
        "name": "vm1",
        "image": "centos6.7",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "status": "active",
        "task": "creating",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "flavor": "m1.large",
        "ha": false,
        "tags": ["private", "production"],
        "created_at": "2016-11-22 10:22:32",
        "disks": [
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol1"
            },
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol2"
            }
        ]
    }
}
```

查看虚拟机详细信息

`GET http://vpe.cds.com/instances/{uuid}`

### Response Body

参数    |  解释
--------|----------
name   | 虚拟机的名称
uuid   | 虚拟机的 uuid
image  | 虚拟机使用的镜像名称
image_uuid| 虚拟机使用的镜像的 uuid
disk_pool | 虚拟机系统盘使用的存储路径的名称
disk_pool_uuid | 虚拟机系统盘使用的存储路径的 uuid
status | 虚拟机状态信息：active, shutoff
task   | 虚拟机当前正在执行的任务：creating, deleting
flavor | 虚拟机使用的配方名称
flavor_uuid | 虚拟机使用的配方的 uuid
ha | 虚拟机是否是高可用模式。高可用虚拟机保证虚拟机永远是上电状态
tags | 虚拟机标签，标签方便对虚拟机进行分类
created_at| 虚拟机的创建时间
disks | 虚拟机挂载的数据盘列表

## Create instance (P0)

```http
POST /instances HTTP/1.1
Accept: application/json

{
    "instance": {
        "name": "vm2",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "disk_pool": "5566a58e-205a-4a93-bd15-409bd2f6f112",
        "ha": true,   # 可选参数，是否高可用，默认为 false
        "tags": ["tag1", "tag2", "tag3"]
        "disks": [    # 可选参数，想要挂载的数据盘，默认为空
            "c588c4d5-9b67-426b-a8d2-e8b0d9be9917",
            "a588c4d5-9b67-426b-a8d2-e8b0d9be9917"
        ]
    }
}

```


```http
HTTP/1.1 200 OK
Content-Type: application/json


{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0",
        "name": "vm2",
        "created_at": "2016-11-22 10:22:32",
        "status": "active",
        "task": "creating",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "disk_pool": "5566a58e-205a-4a93-bd15-409bd2f6f112",
        "ha": true,
        "tags": ["tag1", "tag2", "tag3"],
        "disks": [
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol1"
            },
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol2"
            }
        ]
    }
}

```
> 返回创建的虚拟机 uuid, created_at, status, task 和其他基本信息

创建虚拟机，
`POST http://vpe.cds.com/instances`
该接口为异步接口，虚拟机的状态需要不断调用 `Show instance detail` 接口获取。


## Update instance (P0)

```http
PUT /instances/8d0bd581-7df2-4cd5-aa64-db23c3ac25b0 HTTP/1.1
Content-Type: application/json
Accept: application/json

{
    "instance": {
        "name": "vm2",
        "ha": true,
        "tags": ["tag1", "tag2", "tag3"]
    }
}

```


```http
HTTP/1.1 200 OK
Content-Type: application/json


{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0",
        "name": "vm2",
        "created_at": "2016-11-22 10:22:32",
        "status": "active",
        "task": "creating",
        "flavor_uuid": "d153a654-78bb-49bc-a082-829c598b28a9",
        "image_uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
        "disk_pool": "5566a58e-205a-4a93-bd15-409bd2f6f112",
        "ha": true,
        "tags": ["tag1", "tag2", "tag3"],
        "disks": [
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol1"
            },
            {
                "uuid": "51c03ae4-1c39-4bc6-81c1-07e3600faa65",
                "name": "vol2"
            }
        ]
    }
}

```

修改虚拟机
`PUT http://vpe.cds.com/instances/{uuid}`


## Delete instance (P0)

```http
DELETE /instances/8d0bd581-7df2-4cd5-aa64-db23c3ac25b0 HTTP/1.1
Content-Type: application/json
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0"
    }
}

```
> 返回被删除的虚拟机 uuid

删除虚拟机，
`DELETE http://vpe.cds.com/instances/{uuid}`

## Stop instance (P1)

将虚拟机关机
`POST http://vpe.cds.com/instances/{uuid}/stop`

```http
POST /instances/8d0bd581-7df2-4cd5-aa64-db23c3ac25b0/stop HTTP/1.1
Content-Type: application/json

{}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0"
    }
}
```

## Start instance (P1)

将虚拟机开机
`POST http://vpe.cds.com/instances/{uuid}/start`

```http
POST /instances/8d0bd581-7df2-4cd5-aa64-db23c3ac25b0/start HTTP/1.1
Content-Type: application/json

{}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0"
    }
}
```

## Get VNC (P0)

```http
GET /instances/8d0bd581-7df2-4cd5-aa64-db23c3ac25b0/vnc HTTP/1.1
Content-Type: application/json

{}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "instance": {
        "uuid": "8d0bd581-7df2-4cd5-aa64-db23c3ac25b0",
        "vnc_url": "http://vpe.cds.com/vnc?instance-uuid=8d0bd581-7df2-4cd5-aa64-db23c3ac25b0"
    }
}
```

`GET http://vpe.cds.com/instances/{uuid}/vnc`

## Get instances metrics (P1)

<aside class="warning">To be continue...</aside>
`GET http://vpe.cds.com/instances/{uuid}/metrics`

