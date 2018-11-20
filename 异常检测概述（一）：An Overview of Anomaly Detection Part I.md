# 1 异常检测的问题定义及设定

本部分内容为【3】演讲内容整理，图片来自其演讲ppt，视频在最后的citation有link.
## 1.1 在ML中异常检测问题的定义
1. 给定$x_1,x_2, .... x_N$,每一个$x_i$∈$R^d$
2. 拥有的数据集是混合有正常的点和异常的点
3. 异常的点是由不同生成过程产生的，与正常点不同
## 1.2 三种异常检测的训练设定

1. Supervised : 训练数据集是有标注的，分为正常和异常
2. Clean：所有的训练集都是正常的，测试集中包含有正常和异常的，需要把异常点找出来。
3. Unsupervised：训练是混合正常和异常点的，没有标注的。
## 1.3 WDAD假设 （Well-Defined Anomaly Disturibution）
这假设也就是说，认为异常已经被一个充分定义的分布所描绘，也就是在充足的数据集下，我们应该能找到这个数据集的分布，并把这种异常给发现。
但是这种设想存在着一些问题：
1. 在对抗条件下可能不适用。就像在分类中，正常条件下所训练的模型，可能依赖的特征并不一定真实可靠。在攻击样本经过增加噪音或者调整分布以贴近训练样本的分布，就可能欺骗到模型。
2. 潜在起因的多样性。引起异常的原因可能有多种，也就是异常的表现也可能有多种，并且难以一一列举
3. 用户对于异常的定义的时间变化性。用户对于异常的定义可能会有改变。某一类型的数据在某些时间可能被认为异常，在另外一些时间就不被判定为异常。例如路灯应该在晴天时灭，在黑暗来时关掉，这就是一种表现在不同时间下，被判定的结果的不同。

Supervised的训练方式就是默认了WDAD假设，认为标定的数据能够描摹出异常的分布，但是实际情况下，WDAD假设很难满足，当然在工厂等认为设定的环境可能适用。
Unsupervised：本质上就是聚类，认为异常就是outlier，距离聚类中心较远的点。
Clean: 默认的是异常和正常的分布有较大的差别，所以能够通过分布的差异来判定。
Unsupervised 和 Clean都难以解决下面这样的异常点：
## 1.4 部分难以识别的异常
对于异常点的比例$\alpha$
- 当异常点的比例大于5%时，这就很适合使用二元混合模型。
  - 使用这模型意味着服从了WDAD假设。
  - 混合的部分必须是可分的
  - 混合部分不能在高密度空间（HDR）有较大的重叠，否则无法区分
- 当异常点的较小，如1%、0.1%、0.01%等等，利用突变检测来检测异常
  - 并不需要符合WDAD假设
  - 当异常点并不是突变点或者离异点的时候会失败（当异常分布和正常分布存在重叠或这两者的分布非常相近）
  - 当异常存在着长尾分布，意味着异常的类型多且不集中，难以很好的检测到。

## 1.5 ML做异常检测的方法
主要是采用聚类这样的Unsupervised的方法来做异常检测。主要是通过训练集映射到一个距离度量空间，寻找一个合适的阈值来区分开正常和异常。

目前比较好的方法是周志华老师的Isolation Forest，通过对数据集进行不同维度上的切割，直到所有数据都划分开，或者数据划分到某一个程度。那么异常点总是能够轻易的被划分开来的，因为他们离群。
# 2 Video Anomaly Detection
以下内容主要来自【1】
## 2.1 视频异常检测和ML中的区别
1. ML中的异常检测本质上去解决的是已经经过特征提取的特征向量，寻找其中的异常。然而VAD中的是直接在raw data中寻找异常。
2. VAD包含着对于特征抽取的Encoder的训练和挑取。和ML的数据来源不一样，ML的提取一般采用的是AutoEncoder来获取特征，VAD就不一定了。
3. VAD的对象是Video，video包含着时序信息和空间信息，和ML的处理对象不大相同。需要解决的问题不单单是outlier的识别，还包括一个合适的时序与空间信息的表示学习。

直接raw data去训练数据集，一个理想的feature extractor 应该能够做到特征在空间的分布稀疏，如用Clean的训练方法，认为异常应该散布在特征空间的空隙当中，应能更好的识别。
## 2.2 视频异常检测概况
视频异常检测是一个非监督的学习任务，目标在于发现数据中异常的模式或者动作，这些异常定义是不频繁的或者说是稀有事件。异常是缺乏标记的，自然也缺乏标记数据来训练深层网络。这是相当复杂的任务，毕竟正常点的类包括频繁出现的物体和常规的前景移动。然而异常包括有变化多样的少有的异常事情和没见过的物体等等，这些都被分成一个类。

所以提取视频特征表示的模型可能糅杂了计算机视觉中相当多的方面的内容，包括有动作识别、动作相似度、场景分类、物体识别、视频语义分割、人的姿态评估、人的行为识别和其他一些任务。一个模型完成这个多复杂任务的特征提取。

异常检测是一种无监督的模式识别任务，可以被定义在不同的统计模型中。包括有线性拟合例如PCA，非线性拟合如多种不同类型的自动编码器，和深层生成模型。
【1】中给现有的模型大概分成了三类，主要的区别在于视频的表示学习的差异，分别为重构模型、预测模型和生成模型三种。这将会在下一份blog中细谈。

通过视频的表示学习，自动获取到视频的特征。当采用Clean的训练方法时，认为模型可以描摹出正常的分布情况，异常应该会被较差的重构表示，所以能够通过重构的帧与真实帧的差异来判断是否发生了异常。这一点被【2】反驳了，会在下下份blog中细谈。

## 2.3 视频异常检测的数据集
常用的数据集来自于监控摄像头，这样特点就是，场景是固定的，变化的只是前景，包括有行人的移动，交通的变化。所以这些异常就是主要在于表面上可见的变化和动作的变化。

数据集，现有的数据集主要 在于对表观异常和不自然的运动异常，异常类型相对受限
![上面是经典数据集，下面红框是新数据集 ShanghaiTech](https://img-blog.csdnimg.cn/201811201530516.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpd2lfRnVuZw==,size_16,color_FFFFFF,t_70)
上面是经典数据集，下面红框是新数据集 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120153303699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpd2lfRnVuZw==,size_16,color_FFFFFF,t_70)------

UCSD数据集：一个主体为行人的数据集。异常包括有异常物体的出现：例如骑自行车者和轮椅、车等等。还有行人走在一些并不是常见的地方也会被认为是异常。（包括有两个角度的拍摄，一个是行人在靠近或者远离摄像头、一个是行人在平行摄像头方向移动。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120153322316.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpd2lfRnVuZw==,size_16,color_FFFFFF,t_70)
CUHK  Avenue数据集是学校校园的视频，其中检测的主要是行人的异常动作、错误移动方向、异常物体的出现等。（ICCV2013\16个训练视频、21个测试视频）
还有一些如subway entry and exit dataset等等ShanghaiTech数据集

------
Real-World 数据集
Traffic 数据集【4】
【4】中diss了常用的数据集. “ All the anomalous object shave different appearance from the normal pedestrians in the training data thus can be detected from single frame without motion features. ” 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120153452163.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpd2lfRnVuZw==,size_16,color_FFFFFF,t_70)

【5】中提出了一个更大的数据集，总长超过128h，1900个真实情景下的监控视频数据集，分为13种异常。论文中采用了有监督的训练方法，默认了WDAD，这个就值得商榷，但是更大更真实的数据集对于视频异常检测而言，是个很重要的帮助。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181120154718486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpd2lfRnVuZw==,size_16,color_FFFFFF,t_70)

一家之言，望大佬们斧正~
未完待续。

# 0.引用
【1】 An overview of deep learning based methods for unsupervised and semi-supervised anomaly detection in videos . Journal of Imaging . B.Ravi Kiran ..

【2】 Future Frame Prediction for Anomaly Detection - A New Baseline CVPR 2018

【3】Anomaly Detection: Algorithms, Explanations, Applications. The talk in Microsoft research, 13/3/2018, Thomas Dietterich,[youtube link](https://www.youtube.com/watch?v=12Xq9OLdQwQ)

【4】Spatio-Temporal AutoEncoder for Video Anomaly Detection ACM MM [link](https://www.semanticscholar.org/paper/Spatio-Temporal-AutoEncoder-for-Video-Anomaly-Zhao-Deng/fef6f1e04fa64f2f26ac9f01cd143dd19e549790)

【5】Real-World Anomaly Detection in Surveillance Videos . CVPR 2018
