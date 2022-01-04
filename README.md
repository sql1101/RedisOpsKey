# RedisOpsKey
批量检索redis key 支持正则匹配和删除,支持standalone 和 cluster

#### 已测试环境
* redis 3,redis 6

#### 安装
* python 3
* redis
* redis-py-cluster

#### 使用
1. 基本选项
```
python3 RedisOpsKey.py
usage: RedisOpsKey.py [-h] [--match MATCH] [--host HOST] [--port PORT] [--password PASSWORD] [--mode MODE] [--delete DELETE]

example: python3 RedisOpsKey.py --host 127.0.0.1 --match "a*"

optional arguments:
  -h, --help           show this help message and exit
  --match MATCH        scan match parse default:*
  --host HOST          redis host ip default:127.0.0.1
  --port PORT          redis host port default:6379
  --password PASSWORD  redis host password default:None
  --mode MODE          redis mode, option:standalone(default) or cluster
  --delete DELETE      redis key delete, option:yes or None(default)

```

2. standalone 实例使用
```
###默认输出所有key
python3 RedisOpsKey.py --host 127.0.0.1
foo
a1
goodsId
{foo}bar
k2
a2
bar
a4
database:0 Total Key Number:8


a2
hello
database:2 Total Key Number:2


h1
database:10 Total Key Number:1

###匹配正则
python3 RedisOpsKey.py --host 127.0.0.1 --match "a*"
a1
a2
a4
database:0 Total Key Number:3


a2
database:2 Total Key Number:1

###删除key
python3 RedisOpsKey.py --host 127.0.0.1 --match "a*" --delete yes
a1
del key:a1 success
a2
del key:a2 success
a4
del key:a4 success
database:0 Total Key Number:3


a2
del key:a2 success
database:2 Total Key Number:1
```
3. cluster 实例使用

```
python3 RedisOpsKey.py --host 127.0.0.1 --port 7003 --mode cluster
a
c1
c2
c
b


Total Key Number:5
python3 RedisOpsKey.py --host 127.0.0.1 --port 7003 --mode cluster --match "c"
c


Total Key Number:1
python3 RedisOpsKey.py --host 127.0.0.1 --port 7003 --mode cluster --match "c*"
c1
c2
c


Total Key Number:3
python3 RedisOpsKey.py --host 127.0.0.1 --port 7003 --mode cluster --match "c*" --delete yes
c1
del key:c1 success
c2
del key:c2 success
c
del key:c success


Total Key Number:3
```
