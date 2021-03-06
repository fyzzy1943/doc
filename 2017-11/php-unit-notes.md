# 单元测试笔记

标签：笔记

---

### 单元测试的意义

代码是为了什么，当然是为了重复运行。如何保持unit test代码的稳定？主要靠好的API设计。API切实正确切割了需求，那么在重构的时候API就基本不用变化，unit test也不用重写。以后你重构的时候，只要你的unit test覆盖的够好，基本跑一遍就知道有没有改成傻逼。可以节省大量的时间。 --- 轮子哥
### 什么是可测试的代码

### 手册

https://phpunit.de/manual/6.4/zh_cn/index.html

https://phpunit.de/manual/5.7/zh_cn/index.html

测试

### 版本问题

php5.6 需要用主版本为 5的 phpunit，当前最新版本是 5.7，将在2018年2月2日停止维护。

php7，7.1，7.2 可以使用 phpunit 6。

使用lumen可以直接执行 `vendor/phpunit/phpunit/phpunit` 来运行测试。

## lumen 支持的方法

lumen 自带一些方法，可以帮助我们更方便的测试。

### 接口测试

### 数据库测试

```
public function testDatabase()
{
    // Make call to application...

    $this->seeInDatabase('credit', ['user_id' => 1000]);
}
```

我们可以使用一些方式来使操作不影响到数据库，比如使用事务。在test中使用 `DatabaseTransactions` trait 即可。

```
<?php

use Laravel\Lumen\Testing\DatabaseMigrations;
use Laravel\Lumen\Testing\DatabaseTransactions;

class ExampleTest extends TestCase
{
    use DatabaseTransactions;

    /**
     * A basic functional test example.
     *
     * @return void
     */
    public function testBasicExample()
    {
        $this->get('/foo');
    }
}
```

填充数据库，#### 构造数据

##### 构造 工厂类

参考 `database/factories/ModelFactory.php` 文件。`Faker\Generator` 可以生成随机的符合格式数据。

faker 文档：https://github.com/fzaninotto/Faker

##### 在 test 中使用 工厂类

- 使用 `make` 方法

```
public function testDatabase()
{
    $user = factory('App\User')->make();

    // Use model in tests...
}
```

### !!

在设计程序的时候就要思考怎么测试，程序的依赖关系，确定的输入和输出。同步测试


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTU0NDI2MTcsMTQxMzI1Mzc4MV19
-->