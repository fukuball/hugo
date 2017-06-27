+++
title = "使用 Private Key 登入 AWS EC2"
slug = "shi-yong-private-key-deng-ru-aws-ec2"
date = "2014-04-22T18:22:03.000Z"
url = "/2014/04/22/shi-yong-private-key-deng-ru-aws-ec2"
+++

首先在開 AWS EC2 之前，應該會先取得一組 Private Key，請好好保存這組 Private Key，它會是個 .pem 或 .cer 檔。

開啓 Terminal 之後，請用以下指令登入 AWS EC2：

Step 1：更改 Private Key 檔案權限

	＄chmod 600 path/to/private-key.pem
    
Step 2：使用 SSH 登入 AWS EC2

	$ssh -i path/to/private-key.pem ubuntu@ec2-X-X-X.compute-X.amazonaws.com
    
這樣應該就可以順利登入 AWS EC2 了，其中 Step 1 只要執行過一次就可以了，簡單。