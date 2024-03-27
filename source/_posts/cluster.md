---
title: 使用集群进行计算
categories: 计算机
abbrlink: 1655bff5
---



# 使用集群进行计算

为什么会冒出这么一篇东西呢？

其实这个是我大创的一个副产物。我要训练一个有点大的VAE模型，但是自己电脑跑不动了，所以要使用集群上的gpu节点进行计算嘛。哎呀，发现连怎么交任务都不会。

所以这是名副其实的小白入门教程。

平时用电脑运行程序（比如python程序），常常就是``` python xxx.py``` ，最多前面加一句``` conda activate xx(name of env)```。但是使用集群，你得把任务写成bash脚本交上去！！

以我们的集群为例，用的是jsub进行提交。【用什么提交，不同集群是不一样的。笔者在今年寒假去TDLI冬令营时使用的集群交任务用的就是sbatch。这个具体看超算的文档，一般都能搜到。】师兄很贴心的给集群装了一个插件叫easy_jsub，其实就是对jsub命令进行了一个简化和包装，使得我们可以用一行命令就把任务交上去。

## jsub

交任务之前，先看看可调用的cpu，gpu之类的东西：```jhosts attrib -l``` 

（加多一句，如果跑的东西用到cuda加速，而且只需要某个gpu，.py文件里要加上下面这个）

```
import os 
os.environ['CUDA_VISIBLE_DEVICES'] = 'xxx'  xxx替换为你要的那个gpu
```

利用jsub交任务时，只需把任务写成下面的这个.sh的样子，然后```jsub xxx.sh``` 即可。

完整的用法是：```jsub [OPTIONS] command[argument...]``` 

下面 ---后面的文字是我加的说，自己写脚本的时候记得去掉。这里以运行py文件为例。

```bash
#!/bin/sh	---这一行目的是告诉系统这个文件时bash脚本文件
#JSUB -q normal	---工作队列的名字，一般叫super，rapid，normal之类的，这个具体集群不一样
#JSUB -m gpu01	---调用什么设备运行（这里调用了gpu01）
#JSUB -n 1	---运行多少个节点
#JSUB -e error.%J --- 要是任务报错了，报错信息会输出在这里面。可以改。
#JSUB -o output.%J ---输出的文件，可以改。%J是工作号。
#JSUB -J taskname  ---工作的名字

source xxx ---有时要source一些配置文件，不然集群找不到运行代码的环境。最常用的有source ~./bashrc
conda init ---这行最好加上，不然有可能报错
conda activate xxx ---激活某个特定环境
python main.py 用python运行main.py文件

```

如果用easy_jsub，那么交任务的命令可以写成这样：

```easy_jsub gpu 1 ./test.sh -m gpu02  -o output.%J -name test_task```

gpu对应 -q, 1 对应 -n，

./test.sh 是要运行的bash脚本，把要运行的东西写进去就好。记得加./ ，不可以直接写test.sh，这样系统可能会找不到文件报错。

剩下的不用我解释了吧。

交上去之后会得到一个作业号，之后要查询你的计算任务就要用到。

那交上去之后怎么看任务进程呢？```jjobs``` 或者 ```jjobs -a``` ,找到对应的作业号就好。

```jctrl kill xxx```(xxx为作业号) 可以中断某个任务。



