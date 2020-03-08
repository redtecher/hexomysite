---
title: 树莓派上获取视频数据与笔记本上获取视频的不同
date: 2017-03-15 09:06:44
tags:
- 树莓派
- opencv
categories:
- 树莓派
---

最近做毕业设计要做一个基于机器人视觉的目标识别系统，开始用的stm32，后来速度不够，用上了树莓派。这图像处理第一步就是获取视频数据帧，在这个上面折腾了一会，于是贴出来方便后来者移植使用。

# 使用笔记本获取视频数据
这里可以直接用VideoCapture(0)获取到一个视频对象，cap，cap.read()返回一个布尔值。以及每一帧的对象 frame。方便进行处理
<pre>
import cv2
import numpy as np

cap =cv2.VideoCapture(0)
while(True):
    ret,frame=cap.read()
    gray=cv2.cvtColor(frame,cv2.COLOR_BGR2GRAY)
    cv2.imshow('frame',gray)
    if cv2.waitKey(1) & 0xFF==ord('q'):
        break;
cap.release()
cv2.destroyWindows()
</pre>

# 使用树莓派进行处理 
使用树莓派本来有两种方法，一种是用其自带的raspistill命令，这里推荐使用picamera的python库，十分好用也十分强大。

<pre>
from picamera.array import PiRGBArray
from picamera import PiCamera
import time
import cv2
camera = PiCamera()
camera.resolution = (640, 480)
camera.framerate = 32
rawCapture = PiRGBArray(camera, size=(640, 480))
time.sleep(0.1)
for frame in camera.capture_continuous(rawCapture, format="bgr", use_video_port=True):
    image = frame.array
    #使用获取的帧image进行转换成与笔记本上的frame相同
    cv2.imshow("Frame", image)
    key = cv2.waitKey(1) & 0xFF
    rawCapture.truncate(0)
    if key == ord("q"):
        break



</pre>


# 移植方法
下文中获取的image就是电脑中获取的frame，而后进行处理就行。
但是要注意的是 树莓派上容易报错
需要加上
rawCapture.truncate(0)