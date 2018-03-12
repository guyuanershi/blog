---
title: CS140e-Blinky
tags:
  - CS140e
  - Rust
date: 2018-03-12 22:35:40
---

CS140e是斯坦福大学开设的一门编写操作系统的课程。这个课不同于其他的软件课程，是需要在硬件上搞真的事情。
对我来说比较感兴趣的方面很多：
1. 了解操作系统的一些原理
1. 因为几乎没有在“板子”上开发过东西，所以很好奇 硬件软件之间的联系之类的 ：））
1. 这门课程将用Rust来写程序。Rust是我偶然不知道在哪里看到的，一个新的语言，其目的就是要做一个操作系统的开发语言。
1. 最有意思的是，这门课将用树莓派3（RaspBerry PI3）作为硬件，而我刚好有个，还没想好做些什么，就可以直接用的这门课上。
<!-- more -->

起始第一个任务是做一个小东西让LED灯不停的闪烁。
首先我们要准备好需要的硬件：
1. Raspberry PI 3
1. EL-CK-002 Electonic Fun Kit Bundle with Breadboard Cable Resistor (一个套装包含了所有东西，淘宝可买)
1. CP2102 USB TTL485 TTL232 Adaptor （用来连接电脑和树莓派, 具体的就是USB装TTL232）

## 烤派 （准备硬件）
首先要安装CP2102驱动，否则在Mac上无法识别[下载地址](https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip).
然后在`/dev`下检查是否有`/dev/tty.SLAB_USBtoUART`.

接下来就要认识下树莓派的板子和CP2102的板子，各个脚都是什么，树莓派和CP2102相互怎么接。

| CP2102 Pin | Pi Physical Pin |
|:-----|:-----|
| +5v | 4 |
| GND | 6 |
| RXD | 8 |
| TXD | 10 |

## 读GPIO的文档
GPIO - General Propersal Input/Ouput. GPIO是一种通用的通过高低电平向设备输入/输出的电子针脚。一个GPIO引脚可以是输入也可以是输出，这个是根据设置的电平高低决定的。
树莓派的板子图如下：
{% asset_img PI_Board.png RaspBerry PI 3 Board %}

连接LED到板子上
{% asset_img LED.png Connect LED with PI board %}

OK。接下来就是如何让程序和硬件进行通信了。首先我们要理解一些概念：
+ 一个引脚对应一个内存地址，我们就是要在这个内存地址上赋值，什么值就对应相应的功能
+ 一个内存地址是32位（PI3），所以每一位都有对应这一种开关

此例：
我们用`GPIO16(FSEL16)`，通过查文档[BCM2837 89页](https://web.stanford.edu/class/cs140e/docs/BCM2837-ARM-Peripherals.pdf)。可以知道其对应得寄存器为`register1`，`register1`相应的内存地址为`0x7E200004(GPFSEL1)`。(PI3用的是BCM2835，其物理地址是从`0x3F000000`开始)。
所以首先我们要把`register1`设置成`GPIO16`打开状态：
{% codeblock line_number:false%}
  (volatile unsigned *)(0x3F000000 + 0x200000 + 0x04) = 1 << 18; //左移18位
{% endcodeblock %}
写内存为`*(地址)=value`, register1`的18-20位为`GPIO16`的位置(3bit)，而`001`设成output状态。
## 测试
把写好的程序make一下，然后把编译好的`blinky.bin`改成`kernel8.img`拷贝到PI，插入USB就可以看到LED闪烁了。

## rust code
把相应的C代码改为rust code做相同的操作，得到一致的结果。
rust从地址读写用下面的方式：
{% codeblock line_number:false%}
  const A: *mut u32 = 0x12 as *mut u32; // 地址0x12
  A.read_volatile();                    // 读A的值
  A.write_volatile();                   // 写A的值
{% endcodeblock %}
