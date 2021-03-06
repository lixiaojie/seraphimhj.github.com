<meta http-equiv="content-type" content="text/html; charset=UTF-8">
--- 
layout: post 
title: 用Python实现最小二乘法
tags: [regression, python, least square method]
type: post 
--- 

生活中，我们总是在挖掘事物背后的无形力量，称之为规律的东西。

但是这是非有大智慧，大毅力及大运气而无法达成的，

我们退而求其次，对大量数据进行统计，进而构建模型曲线，利用其去预测下一次的结果。这是机器学习的朴素理解。

我们在这里，简单地，对一些离散点，做一条可表达的函数曲线，使这些点与曲线的误差很小，理想地达到重合的程度，即曲线拟合。 

我们知道，两点确定一条直线，反过来也一样成立。

那么三点呢？二次曲线 

以此类推，如果有N个离散点，我们可以用N次幂的曲线完成理想的拟合。

但，由于计算资源的有限，要找到这样一条曲线，代价太过高昂；因此，实际工程中，经常会采用退化的办法，在代价和精度方面找一个契合点。

我们构造下面的式子描述曲线拟合程度的标准，使拟合曲线yi，与离散点ym差的平方在所有x上最小：

![lsm](/img/l/least-square-method.png)

这种算法叫做**最小二乘拟合**。 

利用python(x,y)提供的库文件，实现这种方法，如下：

    # -*- coding: utf-8 -*-
    import numpy as np
    from scipy.optimize import leastsq
    import pylab as pl
    def func(x, p):
        """
        数据拟合所用的函数: A*sin(2*pi*k*x + theta)
        """
        A, k, theta = p
        return A*np.sin(2*np.pi*k*x+theta)   
    def residuals(p, y, x):
        """
        实验数据x, y和拟合函数之间的差，p为拟合需要找到的系数
        """
        return y - func(x, p)
    x = np.linspace(0, -2*np.pi, 100)
    A, k, theta = 10, 0.34, np.pi/6 # 真实数据的函数参数
    y0 = func(x, [A, k, theta]) # 真实数据
    y1 = y0 + 2 * np.random.randn(len(x)) # 加入噪声之后的实验数据    
    p0 = [7, 0.2, 0] # 第一次猜测的函数拟合参数

    # 调用leastsq进行数据拟合
    # residuals为计算误差的函数
    # p0为拟合参数的初始值
    # args为需要拟合的实验数据
    plsq = leastsq(residuals, p0, args=(y1, x))
    print u"真实参数:", [A, k, theta] 
    print u"拟合参数", plsq[0] # 实验数据拟合后的参数

    pl.plot(x, y0, label=u"真实数据")
    pl.plot(x, y1, label=u"带噪声的实验数据")
    pl.plot(x, func(x, plsq[0]), label=u"拟合数据")

    pl.legend()
    pl.show()

Rock &amp; Roll!

