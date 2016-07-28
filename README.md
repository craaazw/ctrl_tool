crazw-docker-slate
==================


Build
-----
```
docker build -t crazw/slate .
```


Run command
----------

```
docker run -d --name slate \
	-p 4567:4567 \
	-v /Users/crazw/Github/docker/slate/source/slate/:/app/source \
	crazw/slate
```

Custom
------

In your source documentation folder (which looks like [this](https://github.com/tripit/slate/tree/master/source)), create a `Dockerfile` with the following contents:

	FROM tutum/slate

And a `docker-compose.yml` with the following contents:

```shell
version: "2.0"
services:
    slate:
        container_name: slate
        image: crazw/slate
        ports:
            - "4567:4567"
        volumes:
            - /Users/crazw/Github/docker/slate/source/slate/:/app/source

    vpe-api:
        container_name: vpe-api
        image: crazw/slate
        ports:
            - "4500:4567"
        volumes:
            - /Users/crazw/Github/docker/slate/source/vpe-api/:/app/source
```


Use Docker Compose to run it:

    docker-compose up -d

Go to `http://localhost:4567/` and you will see your new API beautiful documentation.


Reference
------
**tutum-docker-slate**：[https://github.com/tutumcloud/slate](https://github.com/tutumcloud/slate)


