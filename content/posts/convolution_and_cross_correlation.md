+++
title = "convolution 和 cross-correlation的区别"
date = 2015-08-20T17:50:49+08:00
tags = ["math"]
categories = ["sci"]
draft = false
+++

“卷积”和“互相关”

<!--more-->


# 计算函数:

- 卷积(convolution)
![卷积函数](/images/convolution_func.png)

- 互相关(cross-correlation)
![互相关函数](/images/cross-correlation_func.png)

# 数学解释:
- cross-correlation是两个时间序列移动不同的相位(lags)后依次求correlation
- convolution和cross-correlation类似, 不过得先将其中一个函数反向再进行计算.

***

# 现实意义:
...


# 代码实现:
## matlab code
```matlab
%matlab
a = [1 5 3 -4 7 -2]
b = [2 3 5 2 -3 -9]
%cross-correlation
[corr_seq lags] = xcorr(a,b)
plot(lags,corr_seq)
%autocorrelation
xcorr(a)
%convolution
...

```
