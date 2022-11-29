
[![Build Status](https://travis-ci.org/jason-gao/YUNDUNSDK.svg?branch=master)](https://travis-ci.org/jason-gao/YUNDUNSDK)
[![Latest Stable Version](https://poser.pugx.org/yundun/yundunsdk/v/stable)](https://packagist.org/packages/yundun/yundunsdk)
[![Total Downloads](https://poser.pugx.org/yundun/yundunsdk/downloads)](https://packagist.org/packages/yundun/yundunsdk)
[![Latest Unstable Version](https://poser.pugx.org/yundun/yundunsdk/v/unstable)](https://packagist.org/packages/yundun/yundunsdk)
[![License](https://poser.pugx.org/yundun/yundunsdk/license)](https://packagist.org/packages/yundun/yundunsdk)
[![Monthly Downloads](https://poser.pugx.org/yundun/yundunsdk/d/monthly)](https://packagist.org/packages/yundun/yundunsdk)
[![Daily Downloads](https://poser.pugx.org/yundun/yundunsdk/d/daily)](https://packagist.org/packages/yundun/yundunsdk)


# YUNDUN API PHP SDK legend

+	接口基地址： 'http://apiv4.yundun.cn/V4/';
+	接口遵循RESTful,默认请求体json,接口默认返回json
+	app_id, app_secret 联系技术客服，先注册一个云盾的账号，用于申请绑定api身份

* 签名
    * 每次请求都签名，保证传输过程数据不被篡改
    * 客户端：sha256签名算法，将参数base64编码+app_secret用sha256签名，每次请求带上签名
    * 服务端：拿到参数用相同的算法签名，对比签名是否正确
    
+   环境要求：php >=5.5
+   依赖composer
         
## 安装

composer require yd/ydsdk

## 使用
```
error_reporting(E_ALL);
ini_set('display_errors', 'on');

require './vendor/autoload.php';

try {
    $config = [
        'app_id'       => getenv('SDK_APP_ID'),
        'app_secret'   => getenv('SDK_APP_SECERT'),
        'base_api_url' => getenv('SDK_API_PRE'),
        //'log'          => true,           //是否记录sdk相关日志
        //'logfileLinux' => '/tmp/sdk.log', //linux日志路径
    ];
    $sdk = new \YunDunSdk\YunDunSdk($config);


    // GET 请求
    $request = [
        'url' => 'test.sdk.get',
        'query' => [
            "page" => 1,
            "pagesize" => 10,
            "data" => [
                "name" => "name名称",
                "domain" => "baidu.com",
            ],
        ],
        'body' => [],
    ];
    $result = $sdk->get($request);
    $jsonData = json_decode($result, 1);
    print_r("api: ".$request['url']."\n");
    print_r("raw: ".$result."\n");
    print_r($jsonData);
    print_r("\n");

    // POST 请求
    $request = [
        'url' => 'test.sdk.post',
        'query' => [],
        'body' => [
            "page" => 1,
            "pagesize" => 10,
            "data" => [
                "name" => "name名称",
                "domain" => "baidu.com",
            ],
        ],
    ];
    $result = $sdk->post($request);
    $jsonData = json_decode($result, 1);
    print_r("api: ".$request['url']."\n");
    print_r("raw: ".$result."\n");
    print_r($jsonData);
    print_r("\n");

    // PATCH 请求
    $request = [
        'url' => 'test.sdk.patch',
        'query' => [],
        'body' => [
            "page" => 1,
            "pagesize" => 10,
            "data" => [
                "name" => "name名称",
                "domain" => "baidu.com",
            ],
        ],
    ];
    $result = $sdk->patch($request);
    $jsonData = json_decode($result, 1);
    print_r("api: ".$request['url']."\n");
    print_r("raw: ".$result."\n");
    print_r($jsonData);
    print_r("\n");

    // PUT 请求
    $request = [
        'url' => 'test.sdk.put',
        'query' => [],
        'body' => [
            "page" => 1,
            "pagesize" => 10,
            "data" => [
                "name" => "name名称",
                "domain" => "baidu.com",
            ],
        ],
    ];
    $result = $sdk->put($request);
    $jsonData = json_decode($result, 1);
    print_r("api: ".$request['url']."\n");
    print_r("raw: ".$result."\n");
    print_r($jsonData);
    print_r("\n");

    // DELETE 请求
    $request = [
        'url' => 'test.sdk.delete',
        'query' => [],
        'body' => [
            "page" => 1,
            "pagesize" => 10,
            "data" => [
                "name" => "name名称",
                "domain" => "baidu.com",
            ],
        ],
    ];
    $result = $sdk->delete($request);
    $jsonData = json_decode($result, 1);
    print_r("api: ".$request['url']."\n");
    print_r("raw: ".$result."\n");
    print_r($jsonData);
} catch(\Exception $e) {
    var_dump("code: " + $e->getCode() + " message: " + $e->getMessage());
}
```

## demo 获取友情链接，如果可以获取到数据，说明api接口可以调通
curl http://apiv4.yundun.com/V4/site.friendlink
