特点

* 人多商品少
* 时间短流量高
* 外挂机器

技术分析

* 瞬时高并发的处理能力
* 多层次的分布式处理能力
* 人机交互与对抗

CDN + LVS

数据库封装类

connect

在connect函数的首尾都调用microtime来记录当前时间，用于后续运行效率分析

同理可以应用到所有执行语句上

```php
  private function Connect($name = 'master')
    {
        global $config;
        $mtime1 = microtime();
        $this->settings = $config['db'][$name];
        $dsn = 'mysql:dbname=' . $this->settings["dbname"] . ';host=' . $this->settings["host"] . '';
        try {
            # Read settings from INI file, set UTF8
            $this->pdo = new \PDO($dsn, $this->settings["user"], $this->settings["password"], array(\PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8;"));

            # We can now log any exceptions on Fatal error.
            $this->pdo->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);

            # Disable emulation of prepared statements, use REAL prepared statements instead.
            $this->pdo->setAttribute(\PDO::ATTR_EMULATE_PREPARES, true);

            # Connection succeeded, set the boolean to true.
            $this->bConnected = true;
        } catch (\PDOException $e) {
            # Write into log
            print_r($e);
            echo $this->ExceptionLog($e->getMessage());
            die();
        }
        $mtime2 = microtime();
        \common\DebugLog::_mysql('connect', null, array('host' => $this->settings['host'], 'dbname' => $this->settings['dbname']), $mtime1, $mtime2, null);
    }
```

调试封装类

1. time性能探针，计算运行的步骤以及每一步的执行效率
2. log日志记录
3. http 接口调用记录以及耗时的汇总统计（数目及时间）
4. redis 调用记录以及耗时的汇总统计
5. mysql 调用记录以及耗时的汇总统计
6. cache 调用记录以及耗时的汇总统计

思考：日志切换开关，见2-8

```php
    /**
     * 是否有可视化界面输出，HTML代码直接返回到浏览器
     */
    public static function _is_show_view() {
        if (self::$instance && isset($_SERVER['HTTP_USER_AGENT'])) {
            return true;
        } else {
            return false;
        }
    }
```

在url里面指定参数，在页面生成debug信息![](/assets/debug_view.png)单商品秒杀

万次秒杀：不需要太多优化，单机mysql即可支持

百万次秒杀： web服务器集群，redis缓存

# 逻辑

库存变化，传递+num或者-num，传递变化量，而不是变化结果。redis用incrby。防止脏数据。

# 优化单机性能

提高页面访问速度

* 减少页面大小，启用gzip压缩：nginx配置
* 减少资源请求数量， 合并和压缩css,js等： minify
* 设置浏览器缓存，利用CDN加速

nginx设置浏览器缓存

```
location ~.*\.(jpg|png|jpeg)$ { #指定缓存文件类型 
  expires 7d;  #设置浏览器过期时间
}
```

提高秒杀接口速度

* 将接口静态化
  * 例子：一共有5万商品，假设涌入1亿人，前50万涌入的人一定能秒杀完，后面的50万到1亿直接访问静态接口，用CDN就能解决
  * 假设一个页面每次访问会产生 50 到 100 次查询（这很常见），但是它又不需要每次都去取最新数据（譬如 app 的首页），这时候就可以用静态化的接口。比如你可以用一个定时器去查询首页需要的数据，然后把查询到的数据组装成一个 JSON 文件保存起来，客户端每次都去查询这个静态的 JSON 文件，这样就可以省下很多次 API 请求。
  * 比如秒杀情况，在秒杀开始前，所有的访问信息都会是错误提示，这个时候我们就可以把后端API的结果用JSON保存起来，客户端每次访问直接返回这个JSON文件。等秒杀开始前删除掉这个JSON文件，返回动态接口。同理可以应用参与秒杀后面的50万到1亿人。
* 快速终止的逻辑放在前面
* 增加冗余的定制化的数据，保证程序更快速



提高数据处理速度

* 数据库索引，一定不能少，更不能乱
* 减少数据规模
  * 如订单数据表，由于历史订单的存在，数据表的规模会越来越大，会减缓查找速度。所以可以考虑专门建一张表用于处理当前活动的订单。结束后再合并到历史订单
* 将数据放到redis缓存中





