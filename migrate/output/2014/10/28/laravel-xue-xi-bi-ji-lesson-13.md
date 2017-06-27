+++
title = "Laravel 學習筆記 Lesson 13"
slug = "laravel-xue-xi-bi-ji-lesson-13"
date = "2014-10-28T11:55:48.000Z"
url = "/2014/10/28/laravel-xue-xi-bi-ji-lesson-13"
draft = true
+++

command

cea

protected $name = 'crawler:fetch-data';

protected $description = 'Use this command to get data from web page.';

public function fire()
	{
		$arguments = $this->argument();
		$file_path = $this->argument('file_path');
		echo "Hello World! Fetch $file_path \n";
	}

app/start/artisan.php

Artisan::add(new CrawlerCommand);

php artisan crawler:fetch_data /var/www/list.txt
Hello World! Fetch /var/www/list.txt

php artisan command:make FooCommand

protected $name = 'foo:bar';

public function fire()
	{
		$arguments = $this->argument();
		print_r($arguments);
		$options = $this->option();
		print_r($options);
		$this->info('Display this on the screen');
		if ($this->confirm('Do you wish to continue? [yes|no]'))
		{
    		$name = $this->ask('What is your name?');
    		$this->info('Your name: '.$name);
		}
	}
    
    
 return array(
			array('a1', InputArgument::REQUIRED, 'An example argument.'),
			array('a2', InputArgument::REQUIRED, 'An example argument.'),
		);
        
 return array(
			array('o1', null, InputOption::VALUE_OPTIONAL, 'An example option.', null),
			array('o2', null, InputOption::VALUE_OPTIONAL, 'An example option.', null),
		);