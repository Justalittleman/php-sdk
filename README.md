# ������Ƶ��PHP-SDK ˵��

## 1 ���

PHP-SDK�����ڷ������˵㲥�ϴ�������������߰����ṩ�򵥡���ݵķ����������û������ϴ���Ƶ��ͼƬ�ļ��Ĺ��ܡ�

## 2 ��������

1. �ļ��ϴ�
2. �ϵ�����

## 3 ����׼��

### 3.1 ��������

1. PHP5.3����֧��Sqlite3
2. ��װcomposerʹ��PHP�����Զ����ػ���

### 3.2 ������

```php
use VideoCloud\Storage\UploadManager;
```

## 4 ʹ��˵��

### 4.1 ��װcomposer

1. windows�ֶ����ذ�װ ����ַ��https://getcomposer.org/doc/00-intro.md

2. ʹ�������а�װ��ϸ��composer����

   ps:�����cmd�����룺composer -version���ְ汾����˵����װ�ɹ�

3. ����composer��Ҫ����Ŀ�ĸ�Ŀ¼�°���һ��`composer.json`���ļ�

   #### composer.json

   ```
   {
       "name": "vcloud/php-sdk",
       "type": "library",
       "description": "VideoCloud Resource (Cloud) Storage SDK for PHP",
       "keywords": ["vcloud", "storage", "sdk", "cloud"],
       "homepage": "http://vcloud.163.com/",
       "license": "MIT",
       "authors": [
           {
               "name": "VideoCloud",
               // "email": "sdk@qiniu.com",
               "homepage": "http://vcloud.163.com/"
           }
       ],
       "require": {
           "php": ">=5.3.3"
       },
       "require-dev": {
           "phpunit/phpunit": "~4.0",
           "squizlabs/php_codesniffer": "~2.3"
       },
       "autoload": {
           "psr-4": {"VideoCloud\\": "phpSDK/src/VideoCloud"},
           "files": ["phpSDK/src/VideoCloud/functions.php"]
       }
   }
   ```

4. ��?`composer.json`?��?`autoload`?�ֶ��������Լ��� autoloader

   **������˵����**

   * `VideoCloud\\`�������ռ�����ƣ�������Ǹ�Ŀ¼
   * `files`����Ҫ�Զ����ص�php�ļ�

5. Ҳ����ֱ�Ӹ���demo�е�`composer.json`�ļ�,����������Ŀ¼��Ҫ�޸ĳ���Ŀ��ӦĿ¼

6. �������Զ����ػ������ļ��ĸ�Ŀ¼�»���һ��`autoload.php`�ļ�

   ```php
   <?php

   function classLoader($class)
   {
       $path = str_replace('\\', DIRECTORY_SEPARATOR, $class);
       $file = __DIR__ . '/src/' . $path . '.php';

       if (file_exists($file)) {
           require_once $file;
       }
   }
   spl_autoload_register('classLoader');

   require_once  __DIR__ . '/src/VideoCloud/functions.php';
   ```

### 4.2  ��ʼ��

������Ƶ�Ƶ㲥����Ҫӵ��һ����Ч�� appKey �� appSecret����ǩ����֤����ͨ�����²����ã�

1. ��ͨ��Ƶ�Ƶ㲥����
2. ��½��Ƶ�ƿ�����ƽ̨��ͨ���������̨->�˻���Ϣ��ȡ appKey �� appSecret��

�ڻ�ȡ�� AppKey �� AppSecret ֮�󣬿ɰ������·�ʽ���г�ʼ����

```js
$uploadMgr = new UploadManager();

$opt=array();
$opt["accessKey"]="your AppKey";
$opt["secretKey"]="your AppSecret";
$opt["trunkSize"]= 2 * 1024 * 1024;

$filePath2 = './birds.mp4';

list($ret, $err) = $uploadMgr->init($opt, $filePath2);
if ($err !== null) {
    die($err);
}
```

**������˵����**

1. $opt["accessKey"]��AppKey
2. $opt["secretKey"]��AppSecret
3. $opt["trunkSize"]����Ƭ��С�����4MB

### 4.3 �ļ��ϴ�

����upload�ӿڣ�����init()����ֵ���ļ�·����������ļ��ϴ���·��֧�����·���������index.js�ļ��������·�����Ƽ�����
ʾ����

```php
list($ret, $err) = $uploadMgr->upload($ret['ret'],$filePath);
```

**������˵����**

1. $ret['ret']Ϊinit()������Ϣ
2. $filePath�ļ����index.js·��

### 4.4 �ϵ�����

upload�ӿ�ͬʱ֧�ֶϵ�������ֻ�贫��init()����ֵ���ļ�·������upload�ӿڼ��ɣ�SDK���Զ���ѯ�ϵ㲢����������
ʾ����

```php
list($ret, $err) = $uploadMgr->upload($ret['ret'],$filePath);
```

**������˵����**

1. $ret['ret']Ϊinit������Ϣ
2. $filePath�ļ����index.js·��

## 5 һ���ϴ�������

```php
<?php
require_once __DIR__ . '/autoload.php';


use VideoCloud\Storage\UploadManager;


$uploadMgr = new UploadManager();


$opt=array();
$opt["accessKey"]="your AppKey";
$opt["secretKey"]="your AppSecret";
$opt["trunkSize"]= 2 * 1024 * 1024;

$filePath = './birds.mp4';

list($ret, $err) = $uploadMgr->init($opt, $filePath);
if ($err !== null) {
    die($err);
}

list($ret, $err) = $uploadMgr->upload($ret['ret'],$filePath);
if ($err !== null) {
    var_dump($err);
} else {
    var_dump($ret);
}
```

## 6 �汾���¼�¼

v1.0.0

1. Node-SDK��ʼ�汾���ṩ�㲥�ϴ��Ļ������ܣ��������ļ��ϴ����ϵ�������

# php-sdk
sdk for upload file to vcloud.163.com
