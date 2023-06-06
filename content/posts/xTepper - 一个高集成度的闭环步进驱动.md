---
title: "xTepper - 一个高集成度的闭环步进驱动"
date: 2023-06-01T00:50:22+08:00
draft: false
tags: ["步进电机","STM32F103","运动控制","i2c"]
categories: ["做点东西","硬件"]
series: []
---
CH340E和USB TypeC用于连接串口进行调试，验证过的程序若无需调试可以不焊接；

AS5600图页上的内容是用于磁编码器反馈的，开环用也可以不焊。

拨码开关可用于配置I2C从机地址等，不用也可以不焊。

功能基本上就是按图页拆分的，酌情裁剪。

电流大的话记得加散热片。

软件也许等我调的完善一些之后会开源。吧。大概。

## 立创开源平台

https://oshwhub.com/san-zhi-chang-jing-lu/xtepper

## 离线备份

生产文件以Gerber形式上传，原理图以PDF形式上传。
[gerber-xtepper.zip](https://www.protodrive.xyz/assets/files/2023-05-29/1685375016-728552-gerber-xtepper.zip )

[schmatic-xtepper.pdf](https://www.protodrive.xyz/assets/files/2023-05-29/1685375100-6252-schmatic-xtepper.pdf  )

[交互式BOM-元件位置](https://www.protodrive.xyz/assets/files/2023-05-29/1685378821-837318-cny.html  )



![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374183-595933-img-20230529-230447.jpg)

![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374188-585475-img-20230529-230454.jpg)	

![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374199-42012-2023-05-29-232503.png)
	
![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374204-841099-2023-05-29-232518.png)	

![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374209-196598-2023-05-29-232636.png)	

![](https://www.protodrive.xyz/assets/files/2023-05-29/1685374212-754815-2023-05-29-2349.png)

