+++
title = "Laravel 學習筆記 Lesson 10"
slug = "laravel-xue-xi-bi-ji-lesson-10"
date = "2014-10-13T07:44:22.000Z"
url = "/2014/10/13/laravel-xue-xi-bi-ji-lesson-10"
draft = true
+++

### 使用 flysystem 串接 aws s3

https://github.com/GrahamCampbell/Laravel-Flysystem

 "graham-campbell/flysystem": "~1.0"
 "league/event": "~1.0"
 "aws/aws-sdk-php": "~2.4"
 
 composer update

app/config/app.php and add the following to the providers key.


'GrahamCampbell\Flysystem\FlysystemServiceProvider'

You can register the Flysystem facade in the aliases key of your app/config/app.php file if you like.

'Flysystem' => 'GrahamCampbell\Flysystem\Facades\Flysystem'

php artisan config:publish graham-campbell/flysystem

'default' => 'local',

$temp_file_path = Input::file('pin_img_file')->getRealPath();
                $file_contents = file_get_contents($temp_file_path);
                Flysystem::put($filename, $file_contents);
                unset($temp_file_path);
                
'awss3' => array(
            'driver'    => 'awss3',
            'key'       => 'your-key',
            'secret'    => 'your-secret',
            'bucket'    => 'your-bucket',
            'region'    => 'your-region',
            // 'base_url'  => 'your-url',
            // 'prefix'    => 'your-prefix',
            // 'eventable' => true,
            // 'cache'     => 'foo'
        ),
        
return Flysystem::getAdapter()->getClient()->getObjectUrl('pin-here.com', $this->pin_img_file, '+5 minutes');