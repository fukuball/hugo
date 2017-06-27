+++
title = "Laravel 學習筆記 Lesson 11"
slug = "laravel-xue-xi-bi-ji-lesson-11"
date = "2014-10-13T08:32:11.000Z"
url = "/2014/10/13/laravel-xue-xi-bi-ji-lesson-11"
draft = true
+++

### 使用 laravel mail 串接 mailgun

"guzzlehttp/guzzle": "~4.0"

先在 app/config/mail.php 設定檔中將 driver 設定為 mailgun

app/config/services.php

'mailgun' => array(
    'domain' => 'your-mailgun-domain',
    'secret' => 'your-mailgun-key',
),

Route::get('/test-mail/{demo}', 'HomeController@getTestMail');

public function getTestMail($demo)
	{

		$to = 'fukuball@gmail.com';
		$to_name = 'Fukuball Lin';
		$subject = 'Welcome!';

		switch ($demo) {

		default:
		case '1':

			$data = array('data1'=>'this is data 1', 'data2'=>'this is data 2');

			Mail::send('emails.welcome-html', $data, function($message) use ($to, $to_name, $subject)
			{
    			$message->to($to, $to_name)->subject($subject);
			});

			echo 'demo 1 mail send';

			break;

		}

	}
    
    
case '2':

			$data = array('data1'=>'this is data 1', 'data2'=>'this is data 2');

			Mail::send(array('emails.welcome-html', 'emails.welcome-text'), $data, function($message) use ($to, $to_name, $subject)
			{
    			$message->to($to, $to_name)->subject($subject);
			});

			echo 'demo 2 mail send';

			break;
            
            
  case '3':

			$data = array('data1'=>'this is data 1', 'data2'=>'this is data 2');

			Mail::send(array('emails.welcome-html', 'emails.welcome-text'), $data, function($message) use ($to, $to_name, $subject, $from, $from_name)
			{
				$message->from($from, $from_name);
    			$message->to($to, $to_name)->cc('fukuball@indievox.com')->subject($subject);
    			$message->attach(public_path().'/robots.txt', array('as' => '檔案名稱'));
			});

			echo 'demo 3 mail send';

			break;