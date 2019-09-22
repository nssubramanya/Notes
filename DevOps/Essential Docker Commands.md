# Essential Docker Commands

### Search Image from Registry - `docker search`
```
$ docker search redis
```

### Launch Container in Background - `docker run`

```
$ docker run -d redis
```

### Find Running Containers - `docker ps`

```
$ docker ps
```
Output:

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
2861ed4d4179        redis               "docker-entrypoint.s…"   27 hours ago        Up 27 hours         6379/tcp            musing_margulis
```

### Inspect Running Container - `docker inspect`

```
$ docker inspect 2861ed4d4179
[
    {
        "Id": "2861ed4d4179fd7821b59886d281a70a5a4bb7c88f78e2d0c18670860c26ca87",
        "Created": "2019-06-18T04:12:03.1652893Z",
        "Path": "docker-entrypoint.sh",
        "Args": [
            "redis-server"

```

### Get logs/messages from container - `docker logs`
Display messages the container has written to standard error or standard out

```
$ docker logs musing_margulis

1:C 18 Jun 2019 04:12:03.804 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 18 Jun 2019 04:12:03.804 # Redis version=5.0.5, bits=64, commit=00000000, modified=0, pid=1, just started
1:C 18 Jun 2019 04:12:03.804 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 18 Jun 2019 04:12:03.805 * Running mode=standalone, port=6379.
```

### Set Container Name & Port - `docker run --name <name> -p <container:local>`

```
docker run -d --name redisHostPort -p 6379:6379 redis:latest

984e564780b98521e6a035296eaa1e270ccc91a9eb0a15eb8afbde837a74b1cf

```

See what's running with `docker ps`

```
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
984e564780b9        redis:latest        "docker-entrypoint.s…"   7 seconds ago       Up 6 seconds        0.0.0.0:6379->6379/tcp   redisHostPort
2861ed4d4179        redis               "docker-entrypoint.s…"   28 hours ago        Up 28 hours         6379/tcp                 musing_margulis
```

### Running on Dynamic Port - `docker run`

```
$ docker run -d --name redisDynamic -p 6379 redis:latest
d231c611a4db3544e6da2d1f1a13f9d29e8d2867faea962139cd1c44126f9a0d
```

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
d231c611a4db        redis:latest        "docker-entrypoint.s…"   4 seconds ago       Up 2 seconds        0.0.0.0:32768->6379/tcp   redisDynamic
984e564780b9        redis:latest        "docker-entrypoint.s…"   6 minutes ago       Up 6 minutes        0.0.0.0:6379->6379/tcp    redisHostPort
2861ed4d4179        redis               "docker-entrypoint.s…"   28 hours ago        Up 28 hours         6379/tcp                  musing_margulis
```

```
$ docker port redisDynamic 7379
Error: No public port '7379/tcp' published for redisDynamic

$ docker port redisDynamic 6379
0.0.0.0:32768
```


