---
typora-root-url: H:\Users\kiwi feng\Desktop\论文笔记\assets
---

# DeepID四代论文笔记

DeepID共包含有四个版本，分别是：

> DeepID1 ：Deep Learning Face Representation from Predicting 10,000 Classes
>
> DeepID2 ：deep learning face representation by joint identification-verification
>
> DeepId2+ ：Deeply learned face representations are sparse, selective, and robust
>
> DeepID3： Face Recognition with Very Deep Neural Networks

本篇笔记在于通读四篇论文，对比其优化的过程。



## DeepID 1: 	Deep Learning Face Representation from Predicting 10,000 Classes

本文旨在提出一个通过深度学习产生一种高维度的特征表示方式。这种表示方式，实在最后一层卷积层经过激活函数后输出的结果，如果后面接上FC，做成classfier。这种特征表示方式可以结合任意的分类器，实现脸部确认。

![1526366869091](1526366869091.png)

上面张图基本就能够涵盖本篇论文的内容。注意到第三第四层卷积层共同下采样组成维度位160的DeepID。第四层的卷积层能够更为全局的提取特征，但由于维度较小，形成一个瓶颈层，容易丢失部分信息，为了克服丢失信息的情况，这里让金字塔的卷积层的第三层与第四层，共同减少可能的信息丢失。

![1526374053144](/1526374053144.png)

图片是被切割成多种类型，39x31xk的长方形图片，31x31xk的正方形图片。文中提出的切割方式如下，虽然size有所不同，但是最终输出的都是160维的数据，当然可以切割更多类型，那么最终产生出来的DeepID总长度就更长了。如下图切割出10种图片，那么最终的DeepID将会1600维的向量，然后根据这个向量输入到一个分类器当中，就可以实现多类别的分类。

（下图虽然看起来图片的大小不同，其实应该在最终只有两类的网络，图片都会经过scale，缩放到长方形尺寸或者正方形尺寸的样子）

![1526373679387](/1526373679387.png)

最后DeepID层采用了一下的函数来将第三层和第四层的输出组合在一起。这里的右上角的标号不是

![1526373903121](/1526373903121.png)

