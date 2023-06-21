这是关于CSPCM backbone改进的代码文件的说明文档

1.CSPCM的核心思想来自<<Patches Are All You Need?>>论文连接:https://arxiv.org/pdf/2201.09792v1.pdf

CSPCM是卷积神经网络具有类似ViT中Transformer中的patches embedding，可以是卷积神经网络具有建模全局特征的能力，针对小目标效果很好。

2.具体用法

1:将CSPCM.py YOLOv5-CSPCM.yaml复制到models文件夹中

2:在models/yolo.py 文件导入CSPCM

from CSPCM import  CSPCM

3:找到models/yolo.py文件下里的parse_model 函数，将CSPCM加入进去

在 for i，(f,n, m， args) in enumerate(d[ 'backbone'] + d[ ' head']):内部对应位置下方只需要增加代码:

```python
        elif m in [CSPCM]:
            c1, c2 = ch[f], args[0]
            if c2 != no:  # if not outputss
                c2 = make_divisible(c2 * gw, 8)
            args = [c1, c2, *args[1:]]

```

然后运行

```python
python train.py --cfg YOLOv5-CSPCM.yaml
```

