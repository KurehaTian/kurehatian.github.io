---
title: "博世BSX-Lite快速上手"
date: 2023-06-06T00:50:22+08:00
draft: false
tags: ["IMU","惯性导航","第三方工具"]
categories: ["第三方工具"]
series: []
---
# 博世BSX-Lite快速上手

## 零、引言

BSX-Lite是博世推出的一款轻量级姿态解算库，可以较为便捷的进行六轴姿态解算，效果还是很不错的。

BSX-Lite进行运算时，只需提供三轴加速度和、三轴角速度与时间戳即可。

截至本文成文，这套库只适用于Arm架构，Armcc编译器。

## 一、引入文件

官方链接：https://www.bosch-sensortec.com/software-tools/software/sensor-fusion-software/

以v1.0.2为例，库的压缩包文件结构为：
```
[Generic]BSXlite_v1.0.2
    |-documentation
    |   |-Integration_guide.pdf                    #参考手册
    |- example                                     #示例文件
    |   |-bsxlite_integration_example.c
    |   |-file_operations.c
    |   |-file_operations.h
    |   |-shortLog_bsxlite.txt
    |-lib                                          #静态库
    |   |-ARMCC_OUT
    |       |-libalgobsxm0
    |       |-libalgobsxm0plus
    |       |-libalgobsxm1
    |       |-libalgobsxm3
    |       |-libalgobsxm4
    |       |-libalgobsxm4fpu
    |       |-libalgobsxm7
    |           （这7个文件夹中都包含）
    |           |-libalgobsx.lib
    |           |-memory_footprint.txt
    |-releasenotes
    |   |-Customer_Release Notes.docx
    |-bsxlite_interface.h                          #接口
```
以Keil编译器，RT1064(Cortex M7)为例。
我们需要将 *bsxlite_interface.h* 和*libalgobsx.lib*引入到项目中去，记得include path中也需要添加。

(p.s.)*libalgobsx.lib*要看你的内核版本，比方说我用的M7的核，所以选文件就选libalgobsxm7\libalgobsx.lib

## 二、移植

强烈建议开始这一步之前先粗读一下手册或者看一下*bsxlite_interface.h*。

### 时间戳
你需要开一个int32类型的全局变量以存储当前时间，单位为微秒。
放在定时器中，在调用陀螺仪之前更新即可。

### 获取数据
从你的陀螺仪中读取数据，并将加速度单位转为m/s^2,角速度单位转为rad/s。

### 建立结构体
bsxlite提供了几种基本的结构体类型，我们需要定义：



| 类型          | 作用       |
| ----------- | ----------- |
| bsxlite_instance_t    | 传感器实例       |
| vector_3d_t              | 加速度向量       |
| vector_3d_t              | 角速度向量       |
| bsxlite_out_t            | 存储输出结果    |

注意这些变量的定义域。

### 初始化
调用*bsxlite_init(bsxlite_instance_t *传感器实例)*函数。

### 传入数据
将以弧度、m/s^2为单位的原始数据存入加速度向量、角速度向量结构体中，下一步备用。

### 计算
调用 *bsxlite_do_step(&传感器实例,微秒时间戳,&加速度输入向量,&角速度输入向量,&输出结果结构体)* 函数。
注意计算更新频率最大只能是100Hz。

### 取结果
之前计算的结果存储在*bsxlite_out_t*类型的结构体中，其中*orientation*是欧拉角输出，单位是弧度。
