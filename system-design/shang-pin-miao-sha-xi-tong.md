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



