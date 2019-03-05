Character-level Convolutional Networks for Text Classification解读
====


## 论文解读

https://blog.csdn.net/irving_zhang/article/details/75634108

https://zhuanlan.zhihu.com/p/51698513

https://blog.csdn.net/liuchonge/article/details/70947995

## 代码

> 代码参考https://github.com/Irvinglove/char-CNN-text-classification-tensorflow ，对其做了调整，可以运行在python3.0环境，运行命令：

```python
python training.py
```

> 其中论文提出了关于卷积结构layer的公式：<a href="https://www.codecogs.com/eqnedit.php?latex=l_{6}&space;=&space;(l_{0}-96)/27" target="_blank"><img src="https://latex.codecogs.com/svg.latex?l_{6}&space;=&space;(l_{0}-96)/27" title="l_{6} = (l_{0}-96)/27" /></a>，各个卷积层的layer过程如下：

```
layer 0: l0 = 1014   batch * 1014 * 70

layer 1: 卷积核       7 * 70 * 1 * 256   l1 = (1014 - 7 + 1)/1 = 1008   batch * 1008 * 1 * 256
         池化         1 * 3 * 1 * 1      l1 = 1008/3 = 336              batch * 336 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 336 * 256 * 1
         
layer 2: 卷积核       7 * 70 * 1 * 256   l2 = (336 - 7 + 1)/1 = 330     batch * 330 * 1 * 256
         池化         1 * 3 * 1 * 1      l2 = 330/3 = 110               batch * 110 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 110 * 256 * 1

layer 3: 卷积核       3 * 70 * 1 * 256   l2 = (110 - 3 + 1)/1 = 108     batch * 108 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 108 * 256 * 1

layer 4: 卷积核       3 * 70 * 1 * 256   l2 = (108 - 3 + 1)/1 = 106     batch * 106 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 106 * 256 * 1

layer 5: 卷积核       3 * 70 * 1 * 256   l2 = (106 - 3 + 1)/1 = 104     batch * 104 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 104 * 256 * 1

layer 6: 卷积核       3 * 70 * 1 * 256   l2 = (104 - 3 + 1)/1 = 102     batch * 102 * 1 * 256
         池化         1 * 3 * 1 * 1      l2 = 102/3 = 34                batch * 34 * 1 * 256
         transpose   [0, 1, 3, 2]                                      batch * 34 * 256 * 1
```
> <a href="https://www.codecogs.com/eqnedit.php?latex=l_{6}&space;=&space;(l_{0}-96)/27&space;=&space;(1014&space;-&space;96)/27&space;=&space;34" target="_blank"><img src="https://latex.codecogs.com/svg.latex?l_{6}&space;=&space;(l_{0}-96)/27&space;=&space;(1014&space;-&space;96)/27&space;=&space;34" title="l_{6} = (l_{0}-96)/27 = (1014 - 96)/27 = 34" /></a>
