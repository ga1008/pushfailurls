## 重推失败的 url 回到 redis 的小工具

----

### 必须：

#### 1. 爬虫多次重试失败的 url 放入 mongodb

#### 2. mongodb 内失败 url 的 key 为 "url"，即 {"url": "www.xxx.com"}

#### 3. 爬虫设置可以使用 redis 的 start_urls

---

### 安装：

```shell script
# 看具体版本，包在 dist 文件夹下
$ pip install pushurls.tar.gz

# 或者安装在线版本
$ pip install pushurls
```

### 使用：

```shell script
# 直接开始：
$ pushurls

# 指定配置文件：
$ pushurls /root/push_fail_urls_set.json
```

### 配置文件格式：(建议直接运行，让程序自动生成配置文件，下次就不必再输入配置)

```json
{"from": [
  {
    "adder_sep": ">>>",
    "condition": {},
    "db": "test_db",
    "from_collection": "test_data",
    "fromdb_str": "127.0.0.1.amazon.test_data",
    "host": "127.0.0.1",
    "password": "123456",
    "port": 27017,
    "source": "admin",
    "url_head": "",
    "url_tail": "**-fixed-**test_url",
    "user": "root"
  }],
  "to": [
  {
    "db": "0",
    "host": "127.0.0.1",
    "port": 6379,
    "spiders": {
      "spider_name1": "S1:start_urls",
      "spider_name2": "S2:start_urls"
    },
    "todb_str": "127.0.0.1:6379.0"
  }]}
```