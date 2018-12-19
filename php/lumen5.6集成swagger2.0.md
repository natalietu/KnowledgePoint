##### 解决 执行php artisan swagger-lume:generate 时，报错：Required @OA\Info() not found 

- 参考文档
    - [DarkaOnLine/L5-Swagger](https://github.com/DarkaOnLine/L5-Swagger)
    - [Laravel5.5中集成Swagger3.0文档](https://caihongtengxu.github.io/2018/08/27/20180827/)


- `composer require "darkaonline/l5-swagger:5.6.*"`
- if you need old @SWG (SWAGGER annotations) support. !!! `composer require 'zircote/swagger-php:2.*'`
- Set environment variable SWAGGER_VERSION to 2.0 in your `.env` file:

        SWAGGER_VERSION=2.0
        
- or in your `config/swagger-lumen.php`:
        
        'swagger_version' => env('SWAGGER_VERSION', '2.0')
        
###### 解决 PHP Fatal error:  Uncaught ReflectionException: Class path.storage does not exist in /Users/natalietu/Webhost/hjscWorkSpace/heroapi/vendor/laravel/framework/src/Illuminate/Container/Container.php:767

- `boostrap/app.php` 添加：
    
        $app->instance('path.storage', app()->basePath() . DIRECTORY_SEPARATOR . 'storage');