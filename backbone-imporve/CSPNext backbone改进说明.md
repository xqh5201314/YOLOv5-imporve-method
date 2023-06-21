这是关于CSPNext backbone改进的代码文件的说明文档

1.CSPNext的核心思想来自<<RTMDet: An Empirical Study of Designing Real-Time Object Detectors>>论文连接:[RTMDet: An Empirical Study of Designing Real-Time Object Detectors | PDF (arxiv.org)](https://arxiv.org/pdf/2212.07784v2.pdf)

CSPNext利用当时将卷积神经网络的卷积核变大的影响，采用5×5的深度可分离卷积替换3×3的普通卷积，可以扩大感受野，提高局部特征交互。

2.具体用法

1:将CSPNext.py YOLOv5-CSPNext.yaml复制到models文件夹中

2:在models/yolo.py 文件导入CSPNeXtLayer

from CSPCM import  CSPNeXtLayer

3:找到models/yolo.py文件下里的parse_model 函数，将CSPNeXtLayer加入进去

在 for i，(f,n, m， args) in enumerate(d[ 'backbone'] + d[ ' head']):内部对应位置下方只需要增加代码:

```python
elif m is CSPNeXtLayer:
            c1, c2 = ch[f], args[0]
            if c2 != no:  # if not output
                c2 = make_divisible(c2 * gw, 8)
            args = [c1, c2, *args[1:]]
            if m in [CSPNeXtLayer]:
                args.insert(2, n)  # number of repeats
                n = 1
```

然后运行

```python
python train.py --cfg YOLOv5-CSPNeXtLayer.yaml
```

