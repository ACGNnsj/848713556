# Exercise_12


---
###1. 摘要
**EXERCISES**

* 5.1 Solve for the potential in the prism geometry in Figure 5.4.

* 5.3 Use the symmetry of the capacitor problem to write a program that obtains the result by calculating the potential in only half of one quadrant of x-y plane.

* 5.6 Calculate the electric potential and field near a lightning rod. Model this as a very long and narrow metal rod held at a high voltage, with one end near a conducting plane. Of special interest is the field near the tip of the rod.

* 5.7 Write two progrems to solve the capacitor problem of Figure 5.6 and 5.7, one using the Jacobi method and one using the SOR algorithm. For a fixed accuracy compare the number of iterations, N_iter, that each algorithm requires as a function of the number of grid elements, L. Show that for the Jacobi method N_iter ~ L^2, while with SOR N_iter ~ L.

---
###2. 背景

* **泊松方程**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;泊松方程（法语：Équation de Poisson）是数学中一个常见于静电学、机械工程和理论物理的偏微分方程，因法国数学家、几何学家及物理学家泊松而得名的。

泊松方程为

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=\Delta&space;\varphi&space;=f" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\Delta&space;\varphi&space;=f" title="\Delta \varphi =f" /></a>
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在这里<a href="http://www.codecogs.com/eqnedit.php?latex=\Delta" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\Delta" title="\Delta" /></a>代表的是拉普拉斯算子，而<a href="http://www.codecogs.com/eqnedit.php?latex=f" target="_blank"><img src="http://latex.codecogs.com/gif.latex?f" title="f" /></a>和<a href="http://www.codecogs.com/eqnedit.php?latex=\varphi" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\varphi" title="\varphi" /></a>可以是在流形上的实数或复数值的函数。当流形属于欧几里得空间，而拉普拉斯算子通常表示为![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/4740f625d7c5f48b7ec29e679a9c13bd10bc5405)，因此泊松方程通常写成

<div align=center>
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/e66b1762dad29817722df3c923e9e6ec29ba1b89" alt="" title="" />
</div>

在三维直角坐标系，可以写成

<div align=center>
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/974dfffb801d29eb9df825bd52833b2034b27c99" alt="" title="" />
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果有<a href="http://www.codecogs.com/eqnedit.php?latex=f\left&space;(&space;x,y,z&space;\right&space;)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?f\left&space;(&space;x,y,z&space;\right&space;)" title="f\left ( x,y,z \right )" /></a>恒等于0，这个方程就会变成一个齐次方程，这个方程称作“拉普拉斯方程”。

热传导方程就是泊松方程的一个著名范例

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Temp_Rod_homobc.svg.png?raw=true" alt="" title="" />
</div>

* **拉普拉斯方程**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;拉普拉斯方程，又名调和方程、位势方程，是一种偏微分方程。因为由法国数学家皮埃尔-西蒙·拉普拉斯首先提出而得名。求解拉普拉斯方程是电磁学、天文学、热力学和流体力学等领域经常遇到的一类重要的数学问题，因为这种方程以势函数的形式描写了电场、引力场和流场等物理对象（一般统称为“保守场”或“有势场”）的性质。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;三维情况下，拉普拉斯方程可由下面的形式描述，问题归结为求解对实自变量x、y、z二阶可微的实函数φ：

使用笛卡尔坐标，

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=\Delta&space;f=\frac{\partial&space;^{2}f}{\partial&space;x^{2}}&plus;\frac{\partial&space;^{2}f}{\partial&space;y^{2}}&plus;\frac{\partial&space;^{2}f}{\partial&space;z^{2}}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\Delta&space;f=\frac{\partial&space;^{2}f}{\partial&space;x^{2}}&plus;\frac{\partial&space;^{2}f}{\partial&space;y^{2}}&plus;\frac{\partial&space;^{2}f}{\partial&space;z^{2}}" title="\Delta f=\frac{\partial ^{2}f}{\partial x^{2}}+\frac{\partial ^{2}f}{\partial y^{2}}+\frac{\partial ^{2}f}{\partial z^{2}}" /></a>
</div>

* **电场**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;电场是存在于电荷周围能传递电荷与电荷之间相互作用的物理场。在电荷周围总有电场存在；同时电场对场中其他电荷发生力的作用。观察者相对于电荷静止时所观察到的场称为静电场。如果电荷相对于观察者运动，则除静电场外，还有磁场出现。除了电荷以外，随着时间流易而变化的磁场也可以生成电场，这种电场叫做涡旋电场或感应电场。迈克尔·法拉第最先提出电场的概念。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![image](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/img874.png?raw=true)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![image](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/250px-VFPt_metal_ball_grounded.svg.png?raw=true)

* **电势**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;电势（electric potential），是静电学里的专有名词，定义为处于电场中某个位置的单位电荷所具有的电势能。电势是标量。其数值不具有绝对意义，只具有相对意义，因此为了便于分析问题，必须设定一个参考位置，并把它设为零，称为零势能点。通常，会把无穷远处的电势设定为零。那么，电势可以定义如下：假设检验电荷从无穷远位置，经过任意路径，克服电场力，缓慢地移动到某位置，则在这位置的电势，等于因迁移所做的机械功与检验电荷量的比值。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;电势必需满足泊松方程，同时符合相关边界条件；假设在某区域内的电荷密度为零，则泊松方程约化为拉普拉斯方程，电势必需满足拉普拉斯方程。
在电动力学里，当含时电磁场存在的时候，电势可以延伸为“广义电势”。特别注意，广义电势不能被视为电势能每单位电荷。

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/electricField.png?raw=true" alt="" title="" />
</div>

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Fig5Blog2.jpg?raw=true" alt="" title="" />
</div>

---
###3. 正文

* **理论推导**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在三维直角坐标系，电势的泊松方程可以写成

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;^&space;2V}{\partial&space;x&space;^&space;2}&space;&plus;&space;\frac{\partial&space;^&space;2V}{\partial&space;y&space;^&space;2}&space;&plus;&space;\frac{\partial&space;^&space;2V}{\partial&space;z&space;^&space;2}&space;=&space;0." target="_blank"><img src="http://latex.codecogs.com/gif.latex?\frac{\partial&space;^&space;2V}{\partial&space;x&space;^&space;2}&space;&plus;&space;\frac{\partial&space;^&space;2V}{\partial&space;y&space;^&space;2}&space;&plus;&space;\frac{\partial&space;^&space;2V}{\partial&space;z&space;^&space;2}&space;=&space;0." title="\frac{\partial ^ 2V}{\partial x ^ 2} + \frac{\partial ^ 2V}{\partial y ^ 2} + \frac{\partial ^ 2V}{\partial z ^ 2} = 0." /></a>
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;其迭代形式为

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=V(i,&space;j,&space;k)&space;=&space;\frac{1}{6}[V(i&space;&plus;&space;1,&space;j,&space;k)&space;&plus;&space;V(i&space;-&space;1,&space;j,&space;k)&space;&plus;&space;V(i,&space;j&space;&plus;&space;1,&space;k)\\&space;&plus;&space;V(i,&space;j&space;-&space;1,&space;k)&space;&plus;&space;V(i,&space;j,&space;k&space;&plus;&space;1)&space;&plus;&space;V(i,&space;j,&space;k&space;-&space;1)]" target="_blank"><img src="http://latex.codecogs.com/gif.latex?V(i,&space;j,&space;k)&space;=&space;\frac{1}{6}[V(i&space;&plus;&space;1,&space;j,&space;k)&space;&plus;&space;V(i&space;-&space;1,&space;j,&space;k)&space;&plus;&space;V(i,&space;j&space;&plus;&space;1,&space;k)\\&space;&plus;&space;V(i,&space;j&space;-&space;1,&space;k)&space;&plus;&space;V(i,&space;j,&space;k&space;&plus;&space;1)&space;&plus;&space;V(i,&space;j,&space;k&space;-&space;1)]" title="V(i, j, k) = \frac{1}{6}[V(i + 1, j, k) + V(i - 1, j, k) + V(i, j + 1, k)\\ + V(i, j - 1, k) + V(i, j, k + 1) + V(i, j, k - 1)]" /></a>
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果约束在一个维度上无限长，则我们可将问题化为二维问题

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=V(i,&space;j,&space;k)&space;=&space;\frac{1}{4}[V(i&space;&plus;&space;1,&space;j,&space;k)&space;&plus;&space;V(i&space;-&space;1,&space;j,&space;k)&space;&plus;&space;V(i,&space;j&space;&plus;&space;1,&space;k)&space;&plus;&space;V(i,&space;j&space;-&space;1,&space;k)]" target="_blank"><img src="http://latex.codecogs.com/gif.latex?V(i,&space;j,&space;k)&space;=&space;\frac{1}{4}[V(i&space;&plus;&space;1,&space;j,&space;k)&space;&plus;&space;V(i&space;-&space;1,&space;j,&space;k)&space;&plus;&space;V(i,&space;j&space;&plus;&space;1,&space;k)&space;&plus;&space;V(i,&space;j&space;-&space;1,&space;k)]" title="V(i, j, k) = \frac{1}{4}[V(i + 1, j, k) + V(i - 1, j, k) + V(i, j + 1, k) + V(i, j - 1, k)]" /></a>
</div>

* **算法探讨**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于求解泊松方程的问题，我们可采用雅可比方法，对于二维问题，其迭代式为

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=V_{new}(i,&space;j)&space;=&space;\frac{1}{4}&space;[V_{old}(i&space;&plus;&space;1,&space;j)&space;&plus;&space;V_{old}(i&space;-1,&space;j)&space;&plus;&space;V_{old}(i,&space;j&space;&plus;&space;1)&space;&plus;&space;V_{old}(i,&space;J&space;-1)]" target="_blank"><img src="http://latex.codecogs.com/gif.latex?V_{new}(i,&space;j)&space;=&space;\frac{1}{4}&space;[V_{old}(i&space;&plus;&space;1,&space;j)&space;&plus;&space;V_{old}(i&space;-1,&space;j)&space;&plus;&space;V_{old}(i,&space;j&space;&plus;&space;1)&space;&plus;&space;V_{old}(i,&space;J&space;-1)]" title="V_{new}(i, j) = \frac{1}{4} [V_{old}(i + 1, j) + V_{old}(i -1, j) + V_{old}(i, j + 1) + V_{old}(i, J -1)]" /></a>
</div>

高斯-赛德尔迭代是对雅克比迭代的改进

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=V_{new}(i,&space;j)&space;=&space;\frac{1}{4}[V_{old}(i&space;&plus;&space;1,&space;j)&space;&plus;&space;V_{new}(i&space;-1,&space;j)&space;&plus;&space;V_{old}(i,&space;J&space;&plus;&space;1)&space;&plus;&space;V_{new}(i,&space;j&space;-&space;1)]" target="_blank"><img src="http://latex.codecogs.com/gif.latex?V_{new}(i,&space;j)&space;=&space;\frac{1}{4}[V_{old}(i&space;&plus;&space;1,&space;j)&space;&plus;&space;V_{new}(i&space;-1,&space;j)&space;&plus;&space;V_{old}(i,&space;J&space;&plus;&space;1)&space;&plus;&space;V_{new}(i,&space;j&space;-&space;1)]" title="V_{new}(i, j) = \frac{1}{4}[V_{old}(i + 1, j) + V_{new}(i -1, j) + V_{old}(i, J + 1) + V_{new}(i, j - 1)]" /></a>
</div>

SOR法则更加先进

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=\Delta&space;V(i,&space;j)&space;=&space;V&space;^&space;{*}(i,&space;j)&space;-&space;V_{old}(i,&space;j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\Delta&space;V(i,&space;j)&space;=&space;V&space;^&space;{*}(i,&space;j)&space;-&space;V_{old}(i,&space;j)" title="\Delta V(i, j) = V ^ {*}(i, j) - V_{old}(i, j)" /></a>
</div>

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=V_{new}(i,&space;j)&space;=&space;\alpha&space;\Delta&space;V(i,&space;j)&space;&plus;&space;V_{old}(i,&space;j)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?V_{new}(i,&space;j)&space;=&space;\alpha&space;\Delta&space;V(i,&space;j)&space;&plus;&space;V_{old}(i,&space;j)" title="V_{new}(i, j) = \alpha \Delta V(i, j) + V_{old}(i, j)" /></a>
</div>

其中

<div align=center>
<a href="http://www.codecogs.com/eqnedit.php?latex=\alpha&space;\approx&space;\frac{2}{1&space;&plus;&space;\pi/L}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?\alpha&space;\approx&space;\frac{2}{1&space;&plus;&space;\pi/L}" title="\alpha \approx \frac{2}{1 + \pi/L}" /></a>
</div>

* **程序模拟**

* Problem 5.1

[查看程序1](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-1.py)

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_1-1.png?raw=true" alt="" title="" />
</div>

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_1-2.png?raw=true" alt="" title="" />
</div>

[查看程序2](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-2.py)

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_1-3.png?raw=true" alt="" title="" />
</div>

* Problem 5.3

问题示意图

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/6b3a46de88b2a64e.png?raw=true" alt="" title="" />
</div>

[查看程序](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-3.py)

等势线如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_2-2.png?raw=true" alt="" title="" />
</div>

等势面如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_2-1.png?raw=true" alt="" title="" />
</div>

俯瞰图如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_2-3.png?raw=true" alt="" title="" />
</div>

电场线如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/2282b7fdf557fb6c.png?raw=true" alt="" title="" />
</div>

放大后局部电场线

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_2-4.png?raw=true" alt="" title="" />
</div>

* Problem 5.6

[查看程序1](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-6.py)

等势线如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_2.png?raw=true" alt="" title="" />
</div>

等势面如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_1.png?raw=true" alt="" title="" />
</div>

[查看程序2](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-5.py)

电场线如下

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/figure_3.png?raw=true" alt="" title="" />
</div>

* Problem 5.7

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;上面已经提及，不同的迭代方案的收敛速度有较大差异，特别是对于较大的系统，利用收敛较快的方法解决偏微分方程问题将节省大量的计算时间。这里展示松弛算法的三个实例——Jacobi、Gauss-Seidel和SOR算法的计算收敛速度。在同样的问题下(平行板电容问题)，对相同的收敛判据，三种方法收敛所需迭代次数展示如图所示。从图中可以看出，SOR方法所需迭代次数最少，且随着计算区域尺度的增加仅仅是线性增大的，另两种方式则是二次方增加的。相应的耗时也展示如下图(b)所示。 

[查看程序](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-7.py)

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/ch5_number.png?raw=true" alt="" title="" />
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如下图所示，SOR方法是将Gauss-Seidel方法中每次更新电位时的增量增加为原来的α倍，选择合适的α可以使电位收敛更快。这里展示了不同α时的迭代次数，可见变化时α确实有单一最小值。

[查看程序](https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/Exercise_12-8.py)

<div align=center>
<img src="https://github.com/ACGNnsj/compuational_physics_N2014301020001/blob/master/Exercise_12/ch5_SOR.png?raw=true" alt="" title="" />
</div>
