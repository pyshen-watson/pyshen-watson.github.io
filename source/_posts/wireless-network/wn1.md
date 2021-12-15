---
title: Wireless.1 無線網路與餘弦波
date: 2021-12-16 00:29:45
index_img: https://i.ibb.co/SKxJfFL/24-5-ways-to-extend-your-wireless-network-9.jpg
banner_img: https://i.ibb.co/SKxJfFL/24-5-ways-to-extend-your-wireless-network-9.jpg
tags: []
categories: [Wireless Network]
math: true
---


# Cosine wave (餘弦波)
    
無限訊號中常使用的**諧波信號(Harmonic signal)**，通常可表示成cosine wave的疊加，最基本的就是：
$$y=cos(\omega t)$$

- $\omega$：Angular frequency (角速度) (常用單位：$rad/s$)
- $t$：Time (時間) (常用單位：$s$)

![可以想像有一個**單位向量**在複平面上旋轉，其與正實數軸的夾角為 $\theta$，$cos(\omega t)$就是此單位向量在實數軸上的投影長度。](https://i.ibb.co/9YNRKQV/image.png)


- $f$：Frequency (頻率) (常用單位：$Hz$)

頻率就是每單位時間轉了幾圈(幾個$2 \pi$)，所以顯然 $\omega = 2 \pi f$

# Initial phase (初始相位)

- $\phi$：Initial phase (初始相位) (常用單位：$rad$)

$$y=cos(\omega t+ \phi)=cos(2 \pi ft+\phi)$$

$+ \phi$ 可以想成：

1. 複平面上**單位向量**一開始就和**正實數軸**夾角為 $\phi$
2. 將餘弦波圖形向**左**平移$\frac{\phi}{2 \pi}$個單位時間

# Euler's formula (歐拉公式)

<img src="https://i.ibb.co/DVQQRQz/image.png" width="20%">
一般來說，我們會以$i$來表示虛數單位$\sqrt{-1}$，但由於$i$在程式語言中經常作為迴圈的index，因此有時候則會使用$j$來做為虛數單位

- $z^*$：Conjugation(共軛複數)

>   $z=a+bi$
>    $z^*=a-bi$

我們可以利用歐拉公式$e^{i\theta}=cos\theta+i\ sin\theta$，將$z=a+bi$ 寫成 $z=d\ e^{i \theta}$ 

> $\theta=tan^{-1}(\frac{b}{a})$ (和正實數軸的夾角)
> $d=\sqrt{a^2+b^2}$ (到原點的距離)

這樣的寫法可以讓複數間的乘法更容易且保持實部與虛部的各自意義

# Propagation(傳播)


## 1. Channel Loss

當sender與receiver距離$d$ ，sender發出強度為$a$ 的餘弦波，且處於**Free Space** (兩者間無阻隔)：

- Sender：$a\ cos(\omega t + \phi)$
- Receiver：$\frac{a}{L} cos(\omega t+ \phi)$

$L$ 將會與$d$ 成正比

## 2. Propagation Delay

由於電波的傳播需要時間，因此兩者間會有時間差$\Delta t$ ，若：

- Sender：$S(t)=cos(\omega t +\phi)$
- Receiver：$R(t) = S(t-\Delta t)=cos(\omega(t-\Delta t)+\phi)=cos(\omega t + (\phi - \phi '))$
    - $\phi'=\omega \Delta t=\omega \frac{d}{c}=2\pi f \frac{d}{c}$
    - 當$f$足夠大時，這個相位差才會變得明顯

## 3. Broadcasting

無線網路是用**廣播(Broadcasting)**來傳播，但如果有多個傳輸端的話，如$S_1(t)$及$S_2(t)$同時發送，那Receiver收到的$R(t)=S_1(t)+S_2(t)$ 將無法分開兩個信號