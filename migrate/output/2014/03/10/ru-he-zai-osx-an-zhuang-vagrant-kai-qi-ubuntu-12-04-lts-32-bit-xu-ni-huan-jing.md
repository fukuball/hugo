+++
title = "如何在 OSX 安裝 Vagrant 開啓 Ubuntu 12.04 LTS 32-bit 虛擬環境"
slug = "ru-he-zai-osx-an-zhuang-vagrant-kai-qi-ubuntu-12-04-lts-32-bit-xu-ni-huan-jing"
date = "2014-03-10T17:09:52.000Z"
url = "/2014/03/10/ru-he-zai-osx-an-zhuang-vagrant-kai-qi-ubuntu-12-04-lts-32-bit-xu-ni-huan-jing"
+++

安裝開發環境一直是個麻煩的問題，因此使用 Vagrant 來無痛安裝一個乾淨的開發環境，將各個 project 所需要的開發環境獨立出來是目前最好的解決方案了。本篇文章將介紹如何在 OSX 上安裝 Vagrant 並開啓 Ubuntu 12.04 LTS 32-bit 虛擬環境。

Step 1：安裝 [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Step 2：安裝 [Vagrant](http://downloads.vagrantup.com/)

Step 3：開一個資料夾來練習

    $ mkdir vagrant-practice
    $ cd vagrant-practice

Step 4：初始化虛擬環境

    $ vagrant init precise32 http://files.vagrantup.com/precise32.box

Step 5：開啟虛擬環境（此步驟會等待比較久的時間，之後執行則會變快）

    $ vagrant up

Step 6：登入虛擬環境

    $ vagrant ssh

如此就有一個全新的 Ubuntu 12.04 LTS 32-bit 虛擬環境了！酷！ 

若想刪除虛擬環境，則執行以下指令：

    $ vagrant destroy
