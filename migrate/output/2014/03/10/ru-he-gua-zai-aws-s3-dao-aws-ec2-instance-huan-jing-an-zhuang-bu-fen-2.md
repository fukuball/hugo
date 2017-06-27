+++
title = "如何掛載 AWS S3 到 AWS EC2 Instance - 環境安裝部份"
slug = "ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-huan-jing-an-zhuang-bu-fen-2"
date = "2014-03-10T17:00:23.000Z"
url = "/2014/03/10/ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-huan-jing-an-zhuang-bu-fen-2"
+++

架構網站服務時，Storage 的規劃也是重要的一環，而 AWS S3 就是一個蠻好的 Storage 服務。

一般常見的做法我們會透過 AWS 提供的 API 來存取 S3 上的檔案，但這樣做並不直覺，而且要通常要將原本存取檔案的程式寫法改成用 S3 API 存取檔案的寫法，有可能會需要修改許多支程式。

所以便有人萌生了將 S3 掛載到 EC2 Instance 的想法，就跟我們買一顆大容量的硬碟裝在電腦上一樣，讓我們的網站服務能夠像在同一部機器存取檔案一樣容易。（其實概念就像我們在實體機器上使用 NFS 來掛載網路硬碟一樣）

環境安裝細節如下：（請確認已開好 S3 bucket，且開好 IAM user 權限）

Step 1：登入 EC2 後使用 sudo 權限

    $ sudo -s

Step 2：先更新 apt-get

    $ apt-get update

Step 3：安裝必要套件

    $ apt-get install make gcc g++ curl libxml2 libxml2-dev libssl-dev libcurl3 libcurl4-gnutls-dev openssl pkg-config

Step 4：進入 /usr/local/src 資料夾

    $ cd /usr/local/src

Step 5：下載 fuse

    $ wget http://sourceforge.net/projects/fuse/files/fuse-2.X/2.9.2/fuse-2.9.2.tar.gz/download -O fuse-2.9.2.tar.gz

Step 6：解壓縮 fuse

    $ tar -xzvf fuse-2.9.2.tar.gz

Step 7：進入 fuse-2.9.2 資料夾

    $ cd fuse-2.9.2

Step 8：編譯安裝 fuse

    $ ./configure --prefix=/usr
    $ make
    $ make install

Step 9：將 fuse 加入 ubuntu kernel

    $ modprobe fuse

Step 10：確認 fuse 是否安裝完成

    $ pkg-config --modversion fuse

Step 11：進入 /usr/local/src 資料夾

    $ cd /usr/local/src

Step 12：下載 s3fs

    $ wget http://s3fs.googlecode.com/files/s3fs-1.71.tar.gz

Step 13：解壓縮 s3fs

    $ tar -xzvf s3fs-1.71.tar.gz

Step 14：進入 s3fs-1.71 資料夾

    $ cd s3fs-1.71

Step 15：編譯安裝 s3fs

    $ ./configure --prefix=/usr
    $ make
    $ make install

完成以上步驟，就可以在 EC2 的 Ubuntu Instance 安裝好可掛載 S3 的環境，關於掛載及卸載部份請見[如何掛載 AWS S3 到 AWS EC2 Instance - 掛載及卸載部份](http://blog.fukuball.com/ru-he-gua-zai-aws-s3-dao-aws-ec2-instance-gua-zai-ji-xie-zai-bu-fen/ "如何掛載 AWS S3 到 AWS EC2 Instance - 掛載及卸載部份") 。