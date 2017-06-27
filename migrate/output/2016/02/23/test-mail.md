+++
title = "Test Mail"
slug = "test-mail"
date = "2016-02-23T13:11:56.000Z"
url = "/2016/02/23/test-mail"
draft = true
+++

```
MAIL_DRIVER=log
```

AuthTest.php
```
	public function setUp() {

        parent::setUp();

        Mail::getSwiftMailer()
            ->registerPlugin(new TestingMailEventListener);

    }
```

AuthTest.php
```
class TestingMailEventListener implements Swift_Events_EventListener
{
    public function beforeSendPerformed($event)
    {
        $message = $event->getMessage();
        dd($message);
    }
}
```

AuthTest.php
```
	public function testSendMail() {
        Mail::raw('Hello World', function($message) {
            $message->to('foo@bar.com');
            $message->from('bar@foo.com');
        });
    }
```

```
dd(get_class_methods($message));
```


```
	protected $mail_messages = [];

	public function setUp() {

        parent::setUp();

        Mail::getSwiftMailer()
            ->registerPlugin(new TestingMailEventListener($this));

    }
```

```
	public function addMailEventMessage(Swift_Message $mail_message)
    {
        $this->mail_messages[] = $mail_message;
    }
```

```
class TestingMailEventListener implements Swift_Events_EventListener
{

    protected $test_case;

    public function __construct($test_case)
    {
        $this->test_case = $test_case;
    }

    public function beforeSendPerformed($event)
    {
        $this->test_case->addMailEventMessage($event->getMessage());
    }
}
```

MialTester.php
```
<?php

trait MailTester
{

    protected $mail_messages = [];

    /** @before **/
    public function setUpMailTester()
    {

        Mail::getSwiftMailer()
            ->registerPlugin(new TestingMailEventListener($this));

    }

    public function addMailEventMessage(Swift_Message $mail_message)
    {
        $this->mail_messages[] = $mail_message;
    }

}

class TestingMailEventListener implements Swift_Events_EventListener
{

    protected $test_case;

    public function __construct($test_case)
    {
        $this->test_case = $test_case;
    }

    public function beforeSendPerformed($event)
    {
        $this->test_case->addMailEventMessage($event->getMessage());
    }
}

```

```
	"autoload-dev": {
        "classmap": [
            "tests/TestCase.php"
        ],
        "files": [
            "tests/MailTester.php"
        ]
    },
```

```
composer dump-autoload
```

```
	public function seeEmailTo($email_to)
    {
        $mail_message = end($this->mail_messages);
        $this->assertArrayHasKey($email_to, $mail_message->getTo());
    }
```

```
<div class="form-group{{ $errors->has('city') ? ' has-error' : '' }}">
    <label class="col-md-4 control-label">City</label>

    <div class="col-md-6">
        <input type="text" class="form-control" name="city" value="{{ old('city') }}">

        @if ($errors->has('city'))
            <span class="help-block">
                <strong>{{ $errors->first('city') }}</strong>
            </span>
        @endif
    </div>
</div>
```