---
title: VisualStudio2019下OpenCV与Eigen配置
date: 2022-3-3 21:21:18
categories: graphics
tags:
---


## OpenCV配置
参考 [VisualStudio2019配置OpenCV4.1.0](https://blog.csdn.net/m0_37360684/article/details/89716881)

## Eigen配置

参考 [VS2019正确的安装Eigen库](https://blog.csdn.net/MaybeTnT/article/details/109841378)

记得将解决方案平台改为X64。

在每次创建新工程时，将F:\Games101\ass0\Ass0\Ass0 下的 OpenCV455x64Debug.props 配置文件复制到新工程中。

头文件内容：

```c++
#include <opencv2/opencv.hpp>
#include <Eigen/Core>
```