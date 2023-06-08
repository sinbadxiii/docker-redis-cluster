# Docker Redis Cluster



## Install
```shell
docker-compose up -d
```

## How use

Example for PHP [predis/predis](https://github.com/predis/predis):

```php 
            $client = new \Predis\Client(
                [
                    [
                        "host" => "127.0.0.1",
                        "port" => 6381
                    ],
                    [
                        "host" => "127.0.0.1",
                        "port" => 6382
                    ],
                    [
                        "host" => "127.0.0.1",
                        "port" => 6383
                    ],
                    [
                        "host" => "127.0.0.1",
                        "port" => 6384
                    ],
                    [
                        "host" => "127.0.0.1",
                        "port" => 6385
                    ],
                    [
                        "host" => "127.0.0.1",
                        "port" => 6386                        
                    ],
                ],
                ['cluster' => 'redis']
            );
        };
```

For Golang [redis/go-redis](https://github.com/redis/go-redis):

```golang
import "github.com/redis/go-redis/v9"

rdb := redis.NewClusterClient(&redis.ClusterOptions{
    Addrs: []string{":6381", ":6382", ":6383", ":6384", ":6385", ":6386"},

    // To route commands by latency or randomly, enable one of the following.
    //RouteByLatency: true,
    //RouteRandomly: true,
})
```

For Python [Grokzen/redis-py-cluster](https://github.com/Grokzen/redis-py-cluster):

```python
>>> from rediscluster import RedisCluster

>>> # Requires at least one node for cluster discovery. Multiple nodes is recommended.
>>> startup_nodes = [{"host": "127.0.0.1", "port": "6381"}, {"host": "127.0.0.1", "port": "6382"}] # ... and etc.
>>> rc = RedisCluster(startup_nodes=startup_nodes, decode_responses=True)

>>> rc.set("foo", "bar")
True
>>> print(rc.get("foo"))
'bar'
```