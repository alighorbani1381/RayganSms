# RayganSms
RayganSms API for send text messages

[![Latest Version on Packagist](https://img.shields.io/packagist/v/trez/raygan-sms.svg?style=flat-square)](https://packagist.org/packages/trez/raygan-sms)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)
[![StyleCI](https://github.styleci.io/repos/164846699/shield?branch=master)](https://github.styleci.io/repos/164846699)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms/?branch=master)
[![Build Status](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms/badges/build.png?b=master)](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms/build-status/master)
[![Code Intelligence Status](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms/badges/code-intelligence.svg?b=master)](https://scrutinizer-ci.com/code-intelligence)
[![Quality Score](https://img.shields.io/scrutinizer/g/farhadmirzapour/RayganSms.svg?style=flat-square)](https://scrutinizer-ci.com/g/farhadmirzapour/RayganSms)
[![Total Downloads](https://img.shields.io/packagist/dt/trez/raygan-sms.svg?style=flat-square)](https://packagist.org/packages/trez/raygan-sms)


<div dir="rtl" align="justify">
    این پکیج امکان اتصال <a href="https://raygansms.com/" target="_blank" >RayganSms API</a> به فریم ورک هایی که جهت نصب پکیج ها از <a href="http://farhadnote.ir/articles/2017/10/29/composer.html" target="_blank" >composer</a> و از استاندارد  <a href="http://farhadnote.ir/articles/2017/10/20/psr.html" target=_blank" >PSR-4</a> جهت <a href="http://farhadnote.ir/articles/2017/11/09/composer-autoloading.html#%D8%B1%D9%88%D8%B4-psr-4-based-autoloading" target="_blank">autoload</a>  نمودن کلاس ها استفاده می نمایند همانند (Laravel,Yii,symfony)   را فراهم می سازد.

## محتوا

- [نصب و پیکره بندی](#نصب-و-پیکره-بندی)
- [نحوه استفاده](#نحوه-استفاده)
- [متدها](#متدها)
- [Laravel](#Laravel)
    - [پیکره بندی در لاراول](#پیکره-بندی-در-لاراول)
    - [نحوه استفاده در لاراول](#نحوه-استفاده-در-لاراول)
    - [استفاده در سیستم اعلانات لاراول ](#استفاده-در-سیستم-اعلانات-لاراول)
- [تولیدکننده](#تولیدکننده)
- [لایسنس](#لایسنس)


## نصب و پیکره بندی  

با استفاده از composer  قادر به نصب این سرویس می باشید:
</div>

```bash
composer require trez/raygan-sms
```

<div dir="rtl">
    
## نحوه استفاده

مطابق کد زیر تنظیمات شناسه، رمزعبور و شماره تماس ارسال کننده را وارد نمائید:
</div>

```php
$user_name = '*******';
$password = '*******';
$phone_number = '*******';;
$sms = new \Trez\RayganSms\Sms($user_name,$password,$phone_number);
```
<div dir="rtl">
    
### متدها

</div>

<div dir="rtl">
    
#### 1- متد ارسال پیامک

</div>

`sendMessage($reciver_number, $text_message)`

<div dir="rtl" >
 مثال :
</div>

```php
echo $sms->sendMessage('0936*******','Test Message');
```

<div dir="rtl" >
    
#### 2- متد ارسال کد احراز هویت 2FA یا  (Two Factor Authentication) 

</div>

`sendAutoAuthCode($reciver_number, $sender_text)`

<div dir="rtl" >
نکته : پارامتر sender_text$ اختیاری می باشد.
</div>
<div dir="rtl" >
 مثال :
</div>

```php
echo $sms->sendAutoAuthCode('0936*******','Welcome ...');
```

<div dir="rtl" >
    
#### 3-  بررسی صحت کد دریافتی احراز هویت ارسال شده توسط کاربر
</div>

`checkAutoAuthCode($reciver_number, $reciver_code)`

<div dir="rtl" >
 مثال :
</div>

```php
$result = $sms->checkAutoAuthCode('0936*******','922387');
if($result){
    ///
}else{
    ///
}
```

<div dir="rtl" >
    
#### 4- متد ارسال کد دلخواه احراز هویت 2FA یا  (Two Factor Authentication)</div>

</div>

`sendAuthCode($reciver_number, $text_message)`

<div dir="rtl" >
 مثال :
</div>

```php
$result = $sms->sendAuthCode('0936*******','hello, your auth: 123456');
```

<div dir="rtl">
    
## Laravel

</div>
<div dir="rtl">
    
### پیکره بندی در لاراول

</div>
<div dir="rtl">
بعد از نصب پکیج ، فایل های config/services.php و env. را مطابق زیر ویرایش نمائید :
</div>

```php
// .env
...
RAYGANSMS_USERNAME=*******
RAYGANSMS_PASSWORD=*******
RAYGANSMS_PHONE_NUMBER=*******
...
```

```php
// config/services.php
...
    'raygansms' => [
        'user_name' => env('RAYGANSMS_USERNAME'),
        'password' => env('RAYGANSMS_PASSWORD'),
        'phone_number' => env('RAYGANSMS_PHONE_NUMBER'),
    ],
...
```
<div dir="rtl">
    چنانچه از نسخه های پایین تر از 5.5 استفاده می نمائید ServiceProvider و aliase  زیر  را به فایل config/app.php اضافه نمائید:
 </div>  
 
 ```php
// config/app.php
...
Trez\RayganSms\RayganSmsServiceProvider::class,
...
'RayganSms' => Trez\RayganSms\Facades\RayganSms::class
...
```

<div dir="rtl">
    
### نحوه استفاده در لاراول

</div>

<div dir="rtl">
    هم اکنون می توانید با استفاده از Facade این پکیج (RayganSms) به متدهای پکیج دسترسی نمایید :
</div>

 ```php
echo  RayganSms::sendMessage('0936*******','Test Message');
    ...   
    
echo  RayganSms::sendAutoAuthCode('0936*******','Welcome ...');
    ...
    
$result = RayganSms::checkAutoAuthCode('0936*******','922387');
if($result){
    ///
}else{
   ///
}
    ...   
    
echo  RayganSms::sendAuthCode('0936*******','hello, your auth: 123456');
    ...
```

<div dir="rtl">
    
###  استفاده در سیستم اعلانات لاراول

</div>

<div dir="rtl">
    جهت استفاده از سیستم اعلانات (<a href="https://laravel.com/docs/5.7/notifications" >Notefications</a>)  لاراول،  پکیج <a href="https://github.com/farhadmirzapour/RaygansmsChannel" >raygan-sms-notification-channel</a>  را نصب و طبق مستندات مربوطه عمل نمائید.
</div>

<div dir="rtl">
    
## تولیدکننده

- [Farhad Mirzapour](https://github.com/farhadmirzapour)
   
## لایسنس


لایسنس این پکیج (MIT) می باشد . جهت اطلاعات در مورد این لایسنس به [License File](LICENSE) مراجعه نمایید. 

</div>

