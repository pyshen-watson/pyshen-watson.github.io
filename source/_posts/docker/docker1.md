---
title: [Docker.1 一些關於Docker的事]
date: 2021-12-15 22:24:41
index_img: https://i.ibb.co/DCg9Dvf/docker.jpg
banner_img: https://i.ibb.co/DCg9Dvf/docker.jpg
categories:
    - [Docker]
tag: [Docker]
---

# 前言
說到為什麼想學Docker，其實老早以前就想學了，只是大部分都只是亂翻翻零散的文章或看一些沒頭沒尾的影片。直到2021的黑色星期五，看到Udemy上的折扣真的太香了，所以買了[Docker Mastery](https://www.udemy.com/course/docker-mastery/)的課程。(這次會好好學的)

至於為什麼要寫成文章呢?一方面是blog上還不知道要寫些什麼，另一方面是我平常習慣使用WSL但他對docker的支援好像滿多問題的。 為了之後換電腦或換工作場所時還能記得怎麼弄這些瑣碎的bug，而不是一直stackoverflow，所以平常就記錄一些debug的過程和筆記吧!

# 安裝
前情提要: 這邊只會提到各種Linux與WSL的安裝方式，其他的我也沒用過。

雖然Docker官方提供了一大堆的說明文件關於不同的Linux該如何安裝到最新版本的Docker，但其實有一個超方便的工具叫做[get.docker.com](https://get.docker.com/)! 我們要做的就只有輸入以下兩行指令:

```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

## 更改 Docker Group權限
雖然是可以用了但目前還只能在root模式下使用，我們可以輸入:

```sh
sudo usermod -aG docker <your_username>
```
來將我們的帳號加入docker group，這樣以後就不用再打`sudo`啦~
這時候我們可以使用:
```sh
docker version
```
來確認docker是否可以使用了， 如果不行的話，可以嘗試log out再log in看看。

## Docker daemon running?
當我們使用`docker version`時，可能會看到這個畫面:

```sh
Client:
 Version:           20.10.11
 API version:       1.41
 Go version:        go1.16.10
 Git commit:        dea9396
 Built:             Thu Nov 18 00:34:03 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

為什麼我們只能看到Client的version呢? 原來WSL並不支援Docker Daemon，解決的方式是到Docker Hub下載[Docker Desktop]。

[原文]提到，下載後需要到Setting > General 勾選 `Expose daemon on tcp://localhost:2375 without TLS`然後在`~/.profile` 中加入 `export DOCKER_HOST=127.0.0.1:2375` 並執行`source ~/.profile` 但我在還沒做這個步驟時，**Docker daemon就已經run起來了**，反而做完這步之後又找不到daemon了@@ 所以大家可以視情況決定要不要加這一步。

## 安裝 Docker Machine
Docker Machine是安裝在各種虛擬化平台，用來管理VM中給Docker Engine運行的Docker Host。
Docker的結構大概長得像這樣:
![](https://i.ibb.co/FbV3pJh/image.png)
不過在後來Docker推出了Docker Desktop之後，就把原本的安裝教學廢棄了，所以我們去Docker Hub下載[Docker Desktop]就好。

## 安裝 Docker Compose
Docker Compose是用來協助定義和共用多容器應用程式而開發的工具，可以用:
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/2.2.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
來完成安裝，也可以到[GitHub](https://github.com/docker/compose)查看最新的release版本。


[Docker Desktop]:https://hub.docker.com/editions/community/docker-ce-desktop-windows
[原文]:https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/wsl-%E8%88%87-windows-%E7%9A%84%E5%AE%8C%E7%BE%8E%E9%9B%99%E7%B5%90%E5%90%88-%E5%9C%A8wsl-%E4%B8%AD%E5%AE%89%E8%A3%9D-docker-e722e87ffa3b