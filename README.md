# DBnet-win10
the test about run DBnet in window

本仓库代码皆来自于官方DBnet项目  https://github.com/MhLiao/DB
本仓库用于在win10系统中运行DBnet的尝试以及相关的代码改动。

# 2023/12/8
跑通了demo代码
具体代码运行问题的解决方法，可以参考我的石墨文档：https://shimo.im/docs/DwqQ9XJvX93qgPxW
如有相关问题，欢迎在Issues中交流和讨论。

# 2024/1/2
补充石墨文档内容

代码库安装报错
1、win10安装shapely报错，找不到geos_c.dll
[win10安装shapely报错，找不到geos_c.dll_loovelj的博客-CSDN博客](https://blog.csdn.net/loovelj/article/details/102796426)

2、pip install editdistance 巴拉巴拉的报错
忘记是怎么做了，好像是从pypi下载后重新安装；或者回退了一个版本，安装的0.5.2

3、OSError: symbolic link privilege not held
用管理员模式运行anaconda prompt

4、ImportError: cannot import name 'deform_conv_cuda'

demo
由于原项目在读取输入数据、模型构建等代码写的比较集成，我暂时没办法将代码分解编写出一个方便的demo代码。因此在demo的时候需要最好用我上传到自己git的代码，上面做了适应window系统的改动（当然会出现其他功能抽筋的可能）。
大致改动内容如下：

代码改动：/concern/log.py  -> 70 
os.syslink(storage_dir, self.log_dir)
->
os.makedirs(self.log_dir)

代码文件夹操作：因为使用demo代码的时候会创建dataset，但是这在demo的过程中是用不上的....可是没文件会报错。所以，需要在如下链接下载数据集，并在根目录创建datasets文件夹，把文件放进去。
https://pan.baidu.com/share/init?surl=BPYxcZnLXN87rQKmz9PFYA   
download code: mz0a
或   https://drive.google.com/open?id=12ozVTiBIqK8rUFWLUrlquNfoQxL2kAl7

模型保存：在如下链接下载预训练模型，在根目录创建path-to-model-directory文件夹，并将预训练模型放入其中。
https://pan.baidu.com/s/1vxcdpOswTK6MxJyPIJlBkA
download code: p6u3
或  https://drive.google.com/open?id=1T9n0HTP3X3Y_nJ0D1ekMhCQRHntORLJG

demo代码：
python demo.py experiments/seg_detector/totaltext_resnet18_deform_thre.yaml --image_path xxx.jpg --resume path-to-model-directory/totaltext_resnet18 --polygon --box_thresh 0.7 --visualize
预测结果会保存在 demo_results文件夹中
