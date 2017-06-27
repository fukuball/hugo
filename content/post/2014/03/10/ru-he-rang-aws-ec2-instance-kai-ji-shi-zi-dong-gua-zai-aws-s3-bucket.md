+++
title = "如何讓 AWS EC2 Instance 開機時自動掛載 AWS S3 Bucket"
slug = "ru-he-rang-aws-ec2-instance-kai-ji-shi-zi-dong-gua-zai-aws-s3-bucket"
date = "2014-03-10T17:06:23.000Z"
url = "/2014/03/10/ru-he-rang-aws-ec2-instance-kai-ji-shi-zi-dong-gua-zai-aws-s3-bucket"
+++

當我們將 S3 bucket 掛到 EC2 instance 時（詳細設定筆記請見：[如何掛載 AWS S3 到 AWS EC2 Instance - 環境安裝部份](https://coderwall.com/p/kdpssg "如何掛載 AWS S3 到 AWS EC2 Instance - 環境安裝部份") 、[如何掛載 AWS S3 到 AWS EC2 Instance - 掛載及卸載部份](https://coderwall.com/p/c8ssvg "如何掛載 AWS S3 到 AWS EC2 Instance - 掛載及卸載部份") ），若將 EC2 instance 重開機，S3 bucket 是不會自動掛載上去的，這時我們可以寫一個 Script 加入排程來讓 EC2 instance 重開機能夠自動掛載 S3 bucket。 

詳細步驟如下：

Step 1：編寫 automount-s3 的 shell script

    $ vim automount-s3

 script 內容：

    sudo mkdir /mnt/s3-drive
    /usr/bin/s3fs <bucketname> <mount-point> -o allow_other

Step 2：將 automount-s3 script 移至 /usr/sbin

    $ sudo mv automount-s3 /usr/sbin

Step 3：更改 automount-s3 script 權限

    $ sudo chown root:root /usr/sbin/automount-s3
    $ sudo chmod +x /usr/sbin/automount-s3

Step 4：將 automount-s3 script 加入 crontab 設定在重新開機時自動執行

    $ crontab -e
 
crontab 內容
   
    @reboot /usr/sbin/automount-s3

完成以上步驟我們就可以讓 EC2 instance 在重新開機時自動掛載 S3 bucket，我們可以實際重新開機測試：

    sudo reboot

重新開機後，我們可以用 df -h 來確認是否有自動掛載：

    $ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/xvda1      7.9G  1.3G  6.3G  17% /
    udev            288M  8.0K  288M   1% /dev
    tmpfs           119M  172K  118M   1% /run
    none            5.0M     0  5.0M   0% /run/lock
    none            296M     0  296M   0% /run/shm
    s3fs            256T     0  256T   0% /mnt/s3-drive

以上就是如何讓 AWS EC2 Instance 在開機時自動掛載 AWS S3 Bucket 的簡易筆記～
