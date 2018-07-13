# 脸部识别三年来顶会论文lists

## 1. ICCV 2017

大多数的论文涉及的是脸部纠正的内容，还有脸部的3D重建，还有就是对于小尺度的脸部检测方面，和视频识别脸部的内容。



1. #### S3FD: Single Shot Scale-Invariant Face Detector(单照片的尺寸比例无关脸部检测器)

   //更多在于解决基于锚定点的检测器随着物体的减小而检测效果恶化的问题

2. Cross-View Asymmetric Metric Learning for Unsupervised Person Re-Identification（跨视图的非对称度量学习的非监督的人员重识别）

   //更多在于Re-ID，但是非对称度量学习可能给脸部的区分有一定的帮助

3. #### Real Time Eye Gaze Tracking With 3D Deformable Eye-Face Model（实时的3D眼脸变形模型的眼睛网格跟踪）

   //6个特征点识别以及3D模型的矫正

4. #### How Far Are We From Solving the 2D & 3D Face Alignment Problem? (And a Dataset of 230,000 3D Facial Landmarks)

   //大数据集+脸部纠正的survey和基于自己数据集的一个2D -3D 的脸部纠正网络

5. ####  Reconstruction-Based Disentanglement for Pose-Invariant Face Recognition（基于重建的姿势无关人脸识别去纠缠）

   //主要是提出一个与姿势无关的特征表示方法，寻找一个丰富的嵌入层来编码个体特征，还有非个体特征。提出一个新的特征的重建度量方法来学习将个体和特征去纠缠。

6. #### Recurrent 3D-2D Dual Learning for Large-Pose Facial Landmark Detection（对于大动作的脸部landmark检测的轮回3D - 2D 的双重学习）

   //解决检测大姿势下的landmark的识别困难，提出3D-2D学习和2D-3D学习的微调方法，循环进行

7. Anchored Regression Networks Applied to Age Estimation and Super Resolution(锚定回归网络应用在年龄估计与超像素)

8. Large Pose 3D Face Reconstruction From a Single Image via Direct Volumetric CNN Regression（通过直接的Volumetric CNN回归在基于单图片的大动作的3D脸部构建）

   //2D - 3D 的3D模型构建

9. Efficient Online Local Metric Adaptation via Negative Samples for Person Re-Identification（通过负样本的高效的在线局部度量调整的行人重识别）

10. #### Beyond Face Rotation: Global and Local Perception GAN for Photorealistic and Identity Preserving Frontal View Synthesis（超越脸部旋转：全局和局部的感知的GAN的真实感和个体保持正面视图推理）

    //GAN和局部特征的截取，利用Encoder和Decoder产生出一个脸部模型纠正，和局部的纠正，组合在一起产生一个整体的脸部，从而进行识别，实现脸部纠正，竟然用GAN 在脸部纠正也是有趣了。

11. #### Detecting Faces Using Inside Cascaded Contextual CNN（利用内部级联上下文CNN检测脸部）

    //好像深圳先进院就爱弄些新结构，内部关联的CNN 的脸与非脸的分类器，提出的是Face Body输入的双源上下文CNN

12. DeepCoder: Semi-Parametric Variational Autoencoders for Automatic Facial Action Coding (用于自动面部动作编码的半参数变分自动编码器）

13. #### Pose-Invariant Face Alignment With a Single CNN（单CNN的动作姿势无关的的脸部纠正）

    //级联、可视化、

14. Unsupervised Domain Adaptation for Face Recognition in Unlabeled Videos（非监督的源适应的无标记视频的脸部识别）

    //视频与拍照的差别在于视频不是每一帧都是清晰的，弥合照片与视频的差别，增强基于脸部图片的网络对于视频帧的存在模糊的帧的识别能力。学习一个与源无关的特征，通过是源生成的区分器（类似GAN的样子

15. Attention-Aware Deep Reinforcement Learning for Video Face Recognition（视频脸部识别的聚焦深度强化学习）

    //主要的目标是把模糊的帧给抛掉，以避免误导网络。图片空间与特征空间共同输入优化脸部信息的使用

16. #### Range Loss for Deep Face Recognition With Long-Tailed Training Data（长尾训练数据的深度脸部识别的范围损失）

    //部分标记个体有较少的图片集，那么把那些称作为长尾，长尾的数据集，以往的论文的做法是把这些数据给抛弃掉的，但是这篇论文的做法引入了range loss 来有效的利用这些数据来训练脸部CNN

17. Learning Dense Facial Correspondences in Unconstrained Images（学习无约束图片中的复杂脸部的关联性）

    //主要提出的是做2D图片对应的3D模型的映射位置的mask，从而可以做到把同一类的脸部图片对应同一个模型的不同位置进行关联。

18. #### Towards Large-Pose Face Frontalization in the Wild （面向自然环境下大姿势的脸部的前向纠正）

    //一个利用GAN 作脸部纠正的一个模型，输入就是3D脸部模型和大动作的变形脸部图片，输出是一张生成的脸部前向纠正图片，然后进行识别。

19. #### Faster Than Real-Time Facial Alignment: A 3D Spatial Transformer Network Approach in Unconstrained Poses（比实时脸部纠正更快：一种在不关联的姿势下的3D 空间变换网络方法）

    //一张2D图片提取3D结构，提出3DSTN，用TPS来变形。识别脸部的关键landmark，然后通过关键点对应TPS变换，对于缺失的信息不人为补充。



## 2. CVPR 2016

1. Face Alignment Across Large Poses: A 3D solution (3D跨大姿势的脸部纠正方法)

2. Face2Face: Real-Time Face Capture and Reenactment of RGB Videos（实时RGB视频的脸部获取与重演）

3. Unconstrained Face Alignment  via Cascaded Compositional Learning（通过级联组合学习的非关联的脸部纠正）

4. Automated 3D Face Reconstruction From Multiple Images Using Quality Measures（利用质量度量从多图片自动3D脸部重建）

5. Occlusion-Free Face Alignment: Deep Regression Networks Coupled With De-Corrupt AutoEncoders（不模糊的脸部纠正：与De-corrupt自动编码器结合的深度回归网络）

6. Joint Training of Cascaded CNN for Face Detection（用于脸部检测的联合训练的级联CNN）

7. Mnemonic Descent Method: A Recurrent Process Applied for End-To-End Face Alignment（记忆复杂的方法：一种循环处理应用在端到端的脸部纠正方法）

8. Large-Pose Face Alignment via CNN-Based Dense 3D  Model Fitting（通过CNN为基础的复杂3D模型适应的大姿势的脸部纠正）

9. Adaptive 3D Face Reconstruction From Unconstrained Photo Collections（从非关联的图片集合中适应性的3D脸部重建）

10. Pose-Aware Face Recognition in the Wild（自然环境下的关注姿势的脸部识别）

11. #### Sparsifying Neural Network Connections for Face Recognition（用于脸部识别的稀疏化的神经网络连接）

12. Latent Factor Guided Convolutional Neural Networks for Age-Invariant Face Recogniton（用于与年龄非相关的由潜在的因素引导的脸部识别CNN ）

13. WIDER FACE : A Face Detection Benchmark（WIDER FACE 一种脸部检测评价数据集）

14. Discriminative Invariant Kernel Features: A Bells-and-Whistles-Free Apporach to Unsupervised Face Recognition and Pose Estimation（有区分的不变的核特征：一种与非重要特征无关的非监督的脸部识别与姿态估计方法）

15. Longitudinal Face Modeling via Temporal Deep Restricted Boltzmann Machines（通过短暂的深度首先的波尔兹曼机的纵向脸部模型）



## 3. CVPR 2017

1. Face Normals "In-The-Wild" Using Fully Convolutional Networks (利用FCN做对于)
2. 