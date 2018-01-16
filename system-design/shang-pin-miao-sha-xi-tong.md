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

