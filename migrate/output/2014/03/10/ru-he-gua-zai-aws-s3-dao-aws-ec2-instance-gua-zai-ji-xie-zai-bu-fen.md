+++
title = "如何掛載 AWS S3 到 AWS EC2 Instance - 掛載及卸載部份"
slug = "ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-gua-zai-ji-xie-zai-bu-fen"
date = "2014-03-10T17:02:29.000Z"
url = "/2014/03/10/ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-gua-zai-ji-xie-zai-bu-fen"
+++

本篇為筆記為如何掛載 AWS S3 到 AWS EC2 Instance 的後續內容，請先閱讀 [如何掛載 AWS S3 到 AWS EC2 Instance - 環境安裝部份](http://blog.fukuball.com/ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-huan-jing-an-zhuang-bu-fen-2/ "如何掛載 AWS S3 到 AWS EC2 Instance - 環境安裝部份") 後再閱讀本篇筆記。

架構網站服務時，Storage 的規劃也是重要的一環，而 AWS S3 就是一個蠻好的 Storage 服務。

一般常見的做法我們會透過 AWS 提供的 API 來存取 S3 上的檔案，但這樣做並不直覺，而且要通常要將原本存取檔案的程式寫法改成用 S3 API 存取檔案的寫法，有可能會需要修改許多支程式。

所以便有人萌生了將 S3 掛載到 EC2 Instance 的想法，就跟我們買一顆大容量的硬碟裝在電腦上一樣，讓我們的網站服務能夠像在同一部機器存取檔案一樣容易。（其實概念就像我們在實體機器上使用 NFS 來掛載網路硬碟一樣）

掛載細節如下：（請確認已開好 S3 bucket，且開好 IAM user 權限，且完成環境安裝）

Step 1：新增 s3fs passwd 檔案

    $ touch /etc/passwd-s3fs

Step 2：編輯 s3fs 檔案

    $ vim /etc/passwd-s3fs

Step 3：填入設定 S3 bucket 時的 bucket name 及設定 IAM user 時得到的 access key id、secret access key

    bucketName:accessKeyID:secretAccessKey

Step 4：更改 s3fs 檔案權限

    $ chmod 640 /etc/passwd-s3fs

Step5：新增 S3 bucket 所要掛載的位置

    $ mkdir /mnt/s3-drive

Step6：將 S3 bucket 掛載上去

    $ /usr/bin/s3fs <bucket-name> /mnt/s3-drive -o allow_other

當完成上述步驟我們就已經將 S3 bucket 掛載到 EC2 的 /mnt/s3-drive 了
我們可以用 df -h 來確認：

    $ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/xvda1      7.9G  1.3G  6.3G  17% /
    udev            288M  8.0K  288M   1% /dev
    tmpfs           119M  172K  118M   1% /run
    none            5.0M     0  5.0M   0% /run/lock
    none            296M     0  296M   0% /run/shm
    s3fs            256T     0  256T   0% /mnt/s3-drive

恭喜！EC2 Instance 多了 256T 的空間了！

若想要卸載 S3 bucket 指令如下：

    $ fusermount -u /mnt/s3-drive

以上就是如何掛載 AWS S3 到 AWS EC2 Instance 的簡易筆記～