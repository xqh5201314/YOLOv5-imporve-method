这是关于SPPF的系列改进包括SimSPPF，SPPCSPC,SimCSPSPPF

SimSPPF为YOLOv6提出的，论文地址:[YOLOv6: A Single-Stage Object Detection Framework for Industrial Applications | PDF (arxiv.org)](https://arxiv.org/pdf/2209.02976v1.pdf)；

SPPCSPC为YOLOv7提出的,论文地址:[YOLOv7: Trainable bag-of-freebies sets new state-of-the-art for real-time object detectors | PDF (arxiv.org)](https://arxiv.org/pdf/2207.02696v1.pdf)；

SimCSPSPPF为YOLOv6 3.0提出的,论文地址：https://arxiv.org/pdf/2301.05586v1.pdf。

具体改进详情见论文。

使用方法:

1.将SPPF_imporve.py复制到models文件夹下

2.在models/yolo.py导入所需模块

from SPPF_imporve import SimSPPF, SPPCSPC, SimCSPSPPF

```
elif m is [SimSPPF，SPPCSPC,SimCSPSPPF]:
            c1, c2 = ch[f], args[0]
            if c2 != no:  # if not output
                c2 = make_divisible(c2 * gw, 8)
            args = [c1, c2, *args[1:]]
            if m in [SimSPPF，SPPCSPC,SimCSPSPPF]:
                args.insert(2, n)  # number of repeats
                n = 1
```

3.进行训练

```python
python train.py --cfg YOLOv5_sppf_imporve.yaml
```

