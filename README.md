# 🍄蘑菇丁 SDK
[![Total Downloads](https://poser.pugx.org/laradocs/moguding/d/total.svg)](https://packagist.org/packages/laradocs/moguding)
[![Latest Stable Version](https://poser.pugx.org/laradocs/moguding/v/stable.svg)](https://packagist.org/packages/laradocs/moguding)
[![Latest Unstable Version](https://poser.pugx.org/laradocs/moguding/v/unstable.svg)](https://packagist.org/packages/laradocs/moguding)
[![License](https://poser.pugx.org/laradocs/moguding/license.svg)](https://packagist.org/packages/laradocs/moguding)

🍄蘑菇丁自动签到|打卡组件

## PHP 版本
PHP 需要 8.0 或以上版本

## 安装

```php
composer require laradocs/moguding
```

## 用法

```php
use Laradocs\Moguding\Client;

$factory = new Client();
/**
 * 用户登录
 * 
 * @param string $driver android|ios
 * @param string $phone 手机号码
 * @param string $password 密码
 * 
 * @return array
 */
$user = $factory->login ( $driver, $phone, $password );
// 登录成功返回的重要数据
[
    "userId"   => "xxx",
    "token"    => "xxx",
    "userType" => "student" // 这里教师账号返回的应该是 teacher，我没测试过
]

/**
 * 获取计划
 * 
 * @param string $token $user [ 'token' ]
 * @param string $userType $user [ 'userType' ]
 * @param int $userId $user [ 'userId']
 * 
 * @return array
 */
$getPlan = $factory->getPlan ( $token, $userType, $userId );
// 获取计划返回的重要数据
[
    "planId" => "xxx",
]

/**
 * 打卡保存
 * 
 * @param string $token $user [ 'token' ]
 * @param string $userId $user [ 'userId' ]
 * @param string $province 省
 * @param string $city 市
 * @param string $address 详细地址（不要带上省和市）
 * @param float $longitude 经度
 * @param float $latitude 纬度
 * @param string $type START|END「注：START: 上班|END: 下班」
 * @param string $device android|ios
 * @param string $planId $getPlan['planId']
 * @param string $description 简介（非必填）
 * @param string $country 国家（默认是中国）
 * 
 * @return array
 */
$save = $factory->save (
    $token,
    $userId,
    $province,
    $city,
    $address,
    $longitude,
    $latitude,
    $type,
    $device,
    $planId,
    $description,
    $country
);
// 打卡保存返回的数据
[
  "code" => 200
  "msg" => "success"
  "data" => [
    "createTime" => "2022-01-15 07:08:49"
    "attendanceId" => "xxxxxxxxxxxxxxxxxxxxxxxx"
  ]
]
```

## 说明

如果有需要更改国家同学可以这么做：

```php
$save = $factory->save (
    ...
    '', // 使用 ''｜"" 做占位符
    '菲律宾'
);
```

如有其它疑问或问题，请在 **Issues** 提出。

## 协作

如果您想参与此项目，请点击右上角的 `Fork` 按钮，我们共同维护此项目。
