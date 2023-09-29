# 来源

https://openaccess.thecvf.com/content/CVPR2023/papers/Wang_MCF_Mutual_Correction_Framework_for_Semi-Supervised_Medical_Image_Segmentation_CVPR_2023_paper.pdf

# 论文阅读

## Abstract

> Semi-supervised learning is a promising method for medical image segmentation under limited annotation. However, the model cognitive bias impairs the segmentation performance, especially for edge regions. Furthermore, current mainstream semi-supervised medical image segmentation (SSMIS) methods lack designs to handle model bias. The neural network has a strong learning ability, but the cognitive bias will gradually deepen during the training, and it is difficult to correct itself. We propose a novel mutual correction framework (MCF) to explore network bias correction and improve the performance of SSMIS. Inspired by the plain contrast idea, MCF introduces two different subnets to explore and utilize the discrepancies between subnets to correct cognitive bias of the model. More concretely, a contrastive difference review (CDR) module is proposed to find out inconsistent prediction regions and perform a review training. Additionally, a dynamic competitive pseudo-label generation (DCPLG) module is proposed to evaluate the performance of subnets in real-time, dynamically selecting more reliable pseudo-labels. Experimental results on two medical image databases with different modalities (CT and MRI) show that our method achieves superior performance compared to several state-of-the-art methods. The code will be available at https://github.com/WYC-321/MCF.

半监督学习是在有限标注（annotation）条件下进行医学图像分割的一种有前途的方法。然而，模型认知偏差会影响分割性能，尤其是边缘区域。此外，目前主流的半监督医学图像分割（SSMIS）方法缺乏处理模型偏差的设计。神经网络具有很强的学习能力，但认知偏差会在训练过程中逐渐加深，而且难以自我纠正。我们提出了一个新颖的相互校正框架（MCF）来探索网络偏差校正，提高 SSMIS 的性能。受朴素对比思想的启发，MCF 引入了两个不同的子网，探索并利用子网之间的差异来纠正模型的认知偏差。更具体地说，我们提出了一个对比差异审查（CDR）模块，以找出不一致的预测区域并进行审查训练。此外，还提出了动态竞争伪标签生成（DCPLG）模块，用于实时评估子网的性能，动态选择更可靠的伪标签。在两个不同模式（CT 和 MRI）的医学图像数据库上的实验结果表明，与几种最先进的方法相比，我们的方法性能更优。代码可在 https://github.com/WYC-321/MCF 上获取。

---

其重点在于，处理了模型中的偏差，并且提出了两种不同的模块：CDR 与 DCPLG

---
## Introduction

![[Mutual Correction Framework-Fig1.png]]

> Making pixel-level annotation is difficult and timeconsuming, especially for medical images. Semisupervised learning is a promising approach for processing images with limited supervised data.
> In recent years, semi-supervised methods based on consistency regularization have attracted the attention of researchers and are one of the mainstream techniques, especially in SSMIS. These methods usually include two subnets, and the general process is to add random perturbations to the same samples and force the subnets to produce consistent prediction results for these perturbed inputs. Mean Teacher (MT) is a typical method among them and inspired a series of SSMIS work. Although these methods have achieved promising results, they ignore the impact of cognitive biases in the model. Cognitive bias is the phenomenon in which the model persists in mispredictions, caused by overfitting to wrong supervision signals. There is evidence that cognitive biases reduce the performance of consistency-regularization-based methods.

进行像素级标注既困难又耗时，尤其是对医学图像而言。半监督学习是利用有限监督数据处理图像的一种有前途的方法。

近年来，基于一致性正则化的半监督方法引起了研究人员的关注，并成为主流技术之一，尤其是在 SSMIS 领域。这些方法通常包括两个子网，一般过程是在相同样本中添加随机扰动，迫使子网对这些扰动输入产生一致的预测结果。Mean Teacher（MT）是其中的一种典型方法，也是 SSMIS 一系列工作的灵感来源。虽然这些方法取得了可喜的成果，但它们忽略了模型中认知偏差的影响。认知偏差是指由于过度拟合错误的监督信号而导致模型持续预测错误的现象。有证据表明，认知偏差会降低基于一致性正则化方法的性能。

---

因为像素标注花费资源，所以一种合理的方案是使用半监督学习，而其使用子网络完成半监督训练，其中 MT 模型是其中一种比较经典的模型，但是其具有认知偏差，会降低一致性正则化的性能。

---

> We take MT-like methods as an example to analyze this issue. As shown `Fig. 1 (a)` the methods based on the MT framework have three features: 
> 	
>> (1) The model consists of teacher and student networks with a shared structure.
>
>> (2) The student network parameters $\theta$ are updated through stochastic gradient descent, while the teacher network parameters ${\theta}'$ are updated from the student network using Exponential Moving Average (EMA) as Eq. (1): ${\theta}' = \alpha{\theta}'+(1-\alpha)\theta$, where $\alpha$ is the EMA decay that controls the updating rate. 
>
>>(3) Consistency regularization is implemented to encourage subnets to produce consistent predictions. Characteristics (1) and (2) naturally give the model a tendency to output consistent predictions. And explicit consistency constraints provide a supervised signal for unlabeled data. Therefore, the above three features make model training simpler and accelerate model convergence.

我们以类似 MT 的方法为例分析这一问题。如图 1 (a)所示，基于 MT 框架的方法有三个特点：

1) 模型由具有共享结构的教师网络和学生网络组成。
2) 学生网络参数 $\theta$ 通过随机梯度下降法更新，而教师网络参数 ${\theta}'$ 则根据学生网络使用指数移动平均法（EMA）更新，如式（1）所示： ${\theta}' = \alpha{\theta}'+(1-\alpha)\theta$ 其中，$\alpha$ 是控制更新速率的 EMA 衰减。
3) 实施一致性正则化，以鼓励子网产生一致的预测。特征（1）和（2）自然会使模型倾向于输出一致的预测结果。而明确的一致性约束则为未标记数据提供了监督信号。因此，上述三个特征使模型训练变得更简单，并加速了模型的收敛。

---

可以注意到 MT 模型的一些基本特征，其中包括一个教师网络以及一个学生网络，其中教师网络使用 EMA（指数移动平均法）更新参数，并且由教师网络生成标签作为学生网络的标注。

---

> However, there are also three limitations hidden in it:
> 
>> (1) Structural sharing among subnets reduces model variability. 
>
>> (2) Due to the parameter update method of EMA, the teacher network is a weighted mixture of the historical states of the student network. Therefore, the performance of the teacher network is constrained by the student network.
>
>> (3) Consistency regularization can also be regarded as a labeling strategy that subnets to generate pseudo-labels for each other. The quality of the pseudo-labels greatly affects the performance of the model. Combining limitations (1) and (2), since the pseudo-labels come from a mixture of historical states with the same architecture as the student network, the consistency-based pseudo-label generation methods are more prone to trap the network in cognitive biases and difficult to correct for mispredictions. In addition, these limitations make the model waste the potential of the multisubnet architecture.

然而，其中也隐藏着三个局限性：

1) 子网之间的结构共享降低了模型的可变性。
2) 由于 EMA 的参数更新方法，教师网络是学生网络历史状态的加权混合物。因此，教师网络的性能受到学生网络的制约。
3) 一致性正则化也可以看作是一种标签策略，即子网络之间相互生成伪标签。伪标签的质量会极大地影响模型的性能。结合局限性（1）和（2），由于伪标签来自与学生网络具有相同架构的历史状态的混合物，基于一致性的伪标签生成方法更容易使网络陷入认知偏差，并且难以纠正错误预测。此外，这些限制还使模型浪费了多子网架构的潜力。

---

同时这种模型存在一些弊端，其中共享结构以及参数的加权混合，本质上教师网络是学生网络的延伸，其二者可能共同陷入同一偏差而无法走出。

---

> To further demonstrate the cognitive bias of the model, we test MT and our proposed MCF every 15 iterations and record the number of erroneous pixels, as shown in Fig. 1 (c). It can be seen that as the training progresses, although the number of bias/wrong pixels continues to decrease, the model overfits some bias predictions that are difficult to correct on its own. The visualization result is shown in Fig. 1 (d). The red mask shows the model’s bias predictions, and the white number shows the number of bias pixels. These bias pixels are mainly located in the target edge region, thus reducing the biased prediction is beneficial to improve the accuracy of edge segmentation. Finally compared with MT, MCF reduces more biased predictions under the same training steps.

为了进一步证明模型的认知偏差，我们每 15 次迭代测试 MT 和我们提出的 MCF，并记录错误像素的数量，如图 1 (c)所示。可以看出，随着训练的进行，虽然偏差/错误像素的数量在不断减少，但模型对一些难以自行纠正的偏差预测进行了过拟合。可视化结果如图 1 (d)所示。红色掩膜表示模型的偏差预测，白色数字表示偏差像素的数量。这些偏差像素主要位于目标边缘区域，因此减少偏差预测有利于提高边缘分割的准确性。最后，与 MT 相比，MCF 在相同的训练步骤下减少了更多的偏差预测。

---

进行了一个比较，本文提出的模型减少了偏差。

---

> In summary, our goal is to find a mechanism for the network to be aware of cognitive biases and correct them. To this end, we propose a mutual correction framework in the semi-supervised medical image segmentation for the exploration of model bias correction. We think that while the network is highly capable of learning, it is difficult to correct biases on its own. Inspired by the idea of contrast, MCF consists of two distinct structural subnets with independent parameter updates, which learn to correct each other through a strong inter-subnet interaction. Specifically, MCF proposes contrastive difference review (CDR) and dynamic competitive pseudo-label generation (DCPLG) for labeled and unlabeled data training, respectively. The CDR takes prediction discrepancies of subnets as potential bias areas and guiding the subnets to correct them. Furthermore, we observe that one of the differences between the medical image segmentation databases and natural image databases is that all medical images are related to the target object. Therefore, it is reasonable to evaluate the performance of the subnets on a small amount of labeled data. Based on this, unlike MT-like methods, MCF does not bind teacher or student roles to fixed subnets, but instead proposes DCPLG to dynamically evaluate and select pseudolabel generation networks for more reliable label propagation. The main contributions of this work are as follows:
> 
>> • We explore the problem of model bias correction and propose a new framework MCF for semi-supervised medical image segmentation.
> 
>> • A CDR module is proposed to guide the network to pay attention and correct its own potential bias.
>
>> • Combined with the characteristics of medical image segmentation databases, DCPLG is proposed to obtain more reliable pseudo-labels.
> 
> We evaluate the proposed MCF framework on semisupervised medical image segmentation with both CT and MRI modalities. Experiments verify the effectiveness of this framework, showing that MCF outperforms the SOTA method, especially in edge segmentation accuracy.

总之，我们的目标是找到一种机制，让网络意识到认知偏差并加以纠正。为此，我们提出了一个半监督医学图像分割中的相互校正框架，用于探索模型偏差校正。我们认为，虽然网络的学习能力很强，但很难独立纠正偏差。受对比思想的启发，MCF 由两个不同的结构子网组成，它们具有独立的参数更新，并通过子网间的强烈互动来相互学习纠正偏差。具体来说，MCF 提出了对比差异审查（CDR）和动态竞争伪标签生成（DCPLG），分别用于有标签和无标签数据的训练。CDR 将子网络的预测差异作为潜在的偏差区域，并引导子网络对其进行修正。此外，我们注意到医学图像分割数据库与自然图像数据库的区别之一在于，所有医学图像都与目标对象相关。因此，在少量标注数据上评估子网的性能是合理的。在此基础上，与类似 MT 的方法不同，MCF 没有将教师或学生角色与固定子网绑定，而是提出了 DCPLG 来动态评估和选择伪标签生成网络，以实现更可靠的标签传播。这项工作的主要贡献如下：

- 我们探讨了模型纠偏问题，并提出了一种用于半监督医学图像分割的新框架 MCF。
- 我们提出了一个 CDR 模块来引导网络关注并纠正自身潜在的偏差。
- 结合医学图像分割数据库的特点，提出了 DCPLG，以获得更可靠的伪标签。

我们在 CT 和 MRI 两种模式的半监督医学图像分割中评估了所提出的 MCF 框架。实验验证了该框架的有效性，表明 MCF 优于 SOTA 方法，尤其是在边缘分割准确性方面。

---

MCF 模型使用 CDR 模块导网络关注并纠正自身潜在的偏差，提出了 DCPLG，动态切换教师与学生网络的角色。

---

## Related Work

### Pseudo-labeling method

> Generating pseudo-labels for unlabeled data is a classic practice in semi-supervised learning. The key point of the pseudo-labeling method is how to generate reliable pseudo-labels. **Pseudo-label** is an early exploration of semi-supervised learning using pseudo-label. This work directly uses a fixed threshold to select high-confidence unlabeled samples for pseudo-labeling. Following Tri-training, Tri-Net is proposed to utilize two subnets to generate pseudo-labels for the third one. In order to improve the quality of pseudo-labels, uncertainty estimation is used in to select more reliable pseudo-labels to improve model performance. Inspired by extreme value theory, the authors **Curriculum labeling: Revisiting pseudolabeling for semi-supervised learning** of propose to use increasing percentage scores to select pseudo-label samples by imitating curriculum learning. These methods lack designs to address bias.

为无标签数据生成伪标签是半监督学习中的一种经典做法。伪标签方法的关键点在于如何生成可靠的伪标签。伪标签是利用伪标签进行半监督学习的早期探索。这项工作直接使用一个固定阈值来选择高置信度的未标记样本进行伪标记。继 Tri-training 之后，Tri-Net 被提出来利用两个子网为第三个子网生成伪标签。为了提高伪标签的质量，使用了不确定性估计来选择更可靠的伪标签，从而提高模型性能。受极值理论的启发，**Curriculum labeling: Revisiting pseudolabeling for semi-supervised learning** 的作者提出通过模仿课程学习，利用百分比分数的增加来选择伪标签样本。这些方法缺乏解决偏差问题的设计。

### Consistency regularization

> In recent years, consistency regularization has become a popular method in semisupervised learning. A representative method, MT, consists of a student network that updates parameters using gradient propagation and a teacher network that updates parameters using EMA. MT performs label propagation by forcing consistent predictions for the perturbed samples. After that, some work inspired by MT appeared. For example, the authors of **Smooth neighbors on teacher graphs for semi-supervised learning** argues that previous consistency methods only consider the perturbations around each data point, while ignoring the connections between data points. Therefore, a graph-based SNTG method is proposed to encourage adjacent points on the teacher graph to maintain consistency against perturbations. In addition, **Virtual adversarial training** introduces adversarial perturbations into consistency learning, however, Verma et al. Finds that adversarial perturbations might impair generalization performance, so an interpolation-consistent training method ICT is proposed by them to avoid this problem. **Tripled-uncertainty guided mean teacher model for semi-supervised medical image segmentation** introduces multitask learning into the MT framework and develops triple uncertainty to guide the student model to learn more reliable predictions from the teacher model. **Semi-supervised neuron segmentation via reinforced consistency learning** proposes a two-stage semi-supervised learning method for neuron segmentation by exploiting the pixel-level prediction consistency between unlabeled samples and their perturbed counterparts. These methods ignore the interactions between subnets and also cannot correct the biases of the network itself.

近年来，一致性正则化已成为半监督学习中的一种流行方法。一种代表性的方法是 MT，它由一个使用梯度传播更新参数的学生网络和一个使用 EMA 更新参数的教师网络组成。MT 通过强制对扰动样本进行一致的预测来执行标签传播。之后，出现了一些受 MT 启发的工作。例如，**Smooth neighbors on teacher graphs for semi-supervised learning** 一书的作者认为，以往的一致性方法只考虑了每个数据点周围的扰动，而忽略了数据点之间的联系。因此，他们提出了一种基于图的 SNTG 方法，鼓励教师图上的相邻点保持一致性以对抗扰动。此外，**Virtual adversarial training** 在一致性学习中引入了对抗扰动，然而，Verma 等人发现对抗扰动可能会损害泛化性能，因此他们提出了插值一致性训练方法 ICT 来避免这一问题。**Tripled-uncertainty guided mean teacher model for semi-supervised medical image segmentation** 将多任务学习引入 MT 框架，并开发了三重不确定性来指导学生模型从教师模型中学习更可靠的预测。**Semi-supervised neuron segmentation via reinforced consistency learning** 提出了一种两阶段半监督学习方法，利用未标记样本与其扰动对应样本之间的像素级预测一致性进行神经元分割。这些方法忽略了子网之间的相互作用，也无法纠正网络本身的偏差。

### Semi-supervised medical image segmentation

> The difficulty of labeled medical image data collection motivates the development of semi-supervised medical image segmentation research. Among these methods, **Local contrastive loss with pseudo-label based self-training for semi-supervised medical image segmentation**, **Reference-guided pseudo-label generation for medical semantic segmentation**, **Semi-supervised left atrium segmentation with mutual consistency training**, **Enhancing pseudo label quality for semi-supervised domain-generalized medical image segmentation** mainly focuses on pseudo-labeling, while **Adaptive hierarchical dual consistency for semi-supervised left atrium segmentation on cross-domain data**, **Transformation-consistent selfensembling model for semisupervised medical image segmentation**, **Semi-supervised medical image segmentation through dualtask consistency**, **Inconsistencyaware uncertainty estimation for semi-supervised medical image segmentation**, **Intra-and inter-pair consistency for semi-supervised gland segmentation** explores the application of consistency regularization. In particular, **Adaptive hierarchical dual consistency for semi-supervised left atrium segmentation on cross-domain data**, **Transformation-consistent selfensembling model for semisupervised medical image segmentation**, **Inconsistencyaware uncertainty estimation for semi-supervised medical image segmentation**, **Intra-and inter-pair consistency for semi-supervised gland segmentation** strives to make the model invariant to samples with different perturbations, while **Semi-supervised medical image segmentation through dualtask consistency** explores consistency between different tasks. In addition, Li et al. Propose a self-ensembling semi-supervised co-training framework for COVID-19 CT segmentation.

标注医学影像数据收集的困难推动了半监督医学影像分割研究的发展。在这些方法中，**Local contrastive loss with pseudo-label based self-training for semi-supervised medical image segmentation**、**Reference-guided pseudo-label generation for medical semantic segmentation**、**Semi-supervised left atrium segmentation with mutual consistency training**、**Enhancing pseudo label quality for semi-supervised domain-generalized medical image segmentation** 主要关注伪标记，而 **Adaptive hierarchical dual consistency for semi-supervised left atrium segmentation on cross-domain data**、**Transformation-consistent selfensembling model for semisupervised medical image segmentation**、**Semi-supervised medical image segmentation through dualtask consistency**、**Inconsistencyaware uncertainty estimation for semi-supervised medical image segmentation**、**Intra-and inter-pair consistency for semi-supervised gland segmentation** 则探讨了一致性正则化的应用。一致性正则化的应用。其中，**Adaptive hierarchical dual consistency for semi-supervised left atrium segmentation on cross-domain data**、**Transformation-consistent selfensembling model for semisupervised medical image segmentation**、**Inconsistencyaware uncertainty estimation for semi-supervised medical image segmentation**、**Intra-and inter-pair consistency for semi-supervised gland segmentation** 致力于使模型对不同扰动的样本保持不变，而 **Semi-supervised medical image segmentation through dualtask consistency** 则探讨了不同任务之间的一致性。此外，Li 等人提出了一种用于 `COVID-19 CT` 分割的自组装半监督协同训练框架。

### Correction learning

> There are several studies exploring error correction related to our method. **Selfsupervised correction learning for semi-supervised biomedical image segmentation** utilizes the multi-task complementary information between inpainting and segmentation to gradually optimize the segmentation results. Some researchers introduce an additional network in the segmentation model to learn the difference between prediction and GT. Specifically, **Mutual learning of complementary networks via residual correction for improving semi-supervised classification** utilizes a complementary correction network to map the output of a base network to GT and guide the training of another base network. **Semi-supervised segmentation based on error-correcting supervision** uses the correction network to judge the matching degree between the segmentations and images, and generates supervised signals for the unlabeled data. These methods require complex loss functions and transformation rules. Different from the above methods, we propose a new framework that does not require additional correction network or complex optimization objectives, which utilizes the internetwork interactions to correct network biases directly.

有几项研究探索了与我们的方法相关的纠错方法。**Selfsupervised correction learning for semi-supervised biomedical image segmentation** 利用内绘和分割之间的多任务互补信息，逐步优化分割结果。一些研究者在分割模型中引入了额外的网络，以学习预测和 GT 之间的差异。具体来说，**Mutual learning of complementary networks via residual correction for improving semi-supervised classification** 利用互补修正网络将基础网络的输出映射到 GT，并指导另一个基础网络的训练。文献 **Semi-supervised segmentation based on error-correcting supervision** 利用校正网络来判断分割与图像之间的匹配程度，并为未标记数据生成监督信号。这些方法都需要复杂的损失函数和变换规则。与上述方法不同，我们提出的新框架不需要额外的校正网络或复杂的优化目标，而是利用互联网络的交互作用直接校正网络偏差。

---

介绍了一些其他的论文在相关领域的工作。

---

## Mutual Correction Framework

![[Mutual Correction Framework-Fig2.png]]

### The Overall process of the MCF

> The training process of MCF is shown in Fig. 2. As mentioned above, MCF consists of two subnets with comparable performance and different structures in our work, denoted by subnet A ($f_A (·)$) and subnet B ($f_B (·)$). In the semi-supervised scenario, the training data contains a small amount of labeled data, denoted by $D_L = {(x_i^L, y_i^L)}_{i=1}^N$, and a large amount of unlabeled data, denoted by $D_u = {(x_i^U)}_{i=N+1}^{N+M}$, where $N << M$. $x_i ∈ ℝ^{H × W × D}$ is the medical volume, and $y_i ∈ \{0,1\}^{H × W × D}$ is the ground-truth. A batch of input data $X$ contains equal labeled data ($X^L, Y^L$) and unlabeled data $X^U$, and these volumes are sent to subnet A and subnet B:
> $$\hat{Y}_A = f_A (X)\quad\hat{Y}_B = f_B (X)$$
> The outputs include labeled and unlabeled volume predictions: $\hat{Y} = \hat{Y}^L ∪ \hat{Y}^U$. Note that the subnet index subscripts are omitted here for brevity. The loss function of the subnets $L_{subnet}$ includes supervised loss and unsupervised loss. Specifically, for labeled data prediction $\hat{Y}^L$, except for the conventional segmentation loss (i.e., $L_{dice}$ and $L_{ce}$), a rectification loss $L_{rec}$ is also introduced through CDR for potential misprediction correction. For unlabeled data prediction $\hat{Y}^U$, DCPLG is used to dynamically generate pseudo-labels to supervise the non-pseudo-label generation subnet by unsupervised loss $L_u$. The heterogeneous subnet structure and independent parameter update introduce more diversity to the MCF, fully unlocking the potential of the multi-subnet architecture.

MCF 的训练过程如图 2 所示。如前所述，MCF 由两个子网络组成，在我们的工作中性能相近但结构不同，分别表示为子网络 A（$f_A (·)$）和子网络 B（$f_B (·)$）。在半监督场景中，训练数据包含少量标记数据，表示为 $D_L = {(x_i^L, y_i^L)}_{i=1}^N$，以及大量未标记数据，表示为 $D_u = {(x_i^U)}_{i=N+1}^{N+M}$，其中 $N << M$。$X_i ∈ ℝ^{H × W × D}$ 是医学体积，$y_i ∈ \{0,1\}^{H × W × D}$ 是真实值。输入数据 X 的批次包含相等的标记数据（$X^L, Y^L$）和未标记数据 $X^U$，这些体积被发送到子网络 A 和子网络 B：

$$\hat{Y}_A = f_A (X)\quad\hat{Y}_B = f_B (X)$$

输出包括标记和未标记的体积预测：$\hat{Y} = \hat{Y}^L ∪ \hat{Y}^U$。为了简洁起见，这里省略了子网索引下标。子网络的损失函数 $L_{subnet}$ 包括监督损失和无监督损失。具体来说，对于标记数据的预测 $\hat{Y}^L$，除了传统的分割损失（即 $L_{dice}$ 和 $L_{ce}$），还通过 CDR 引入了校正损失 $L_{rec}$，用于潜在的错误预测校正。对于未标记数据的预测 $\hat{Y}^U$，使用 DCPLG 动态生成伪标签，通过无监督损失 $L_u$ 监督非伪标签生成子网。异构的子网结构和独立的参数更新为 MCF 引入了更多的多样性，充分发挥了多子网络架构的潜力。"

---

讲述了 MCF 的训练过程。

---

### Contrastive discrepancy review（对照差异评估）

> The process of CDR is shown in Fig. 3. CDR is inspired by a simple truth: in a binary classification scenario, if two classifiers have different predictions for the same voxel, then one of them must be wrong. Therefore, we treat the inconsistent predictions as possible areas of misprediction and let the network review these areas. The misprediction area masks can be obtained by the XOR with binarization between the softmax output $\hat{Y}^{U}$ of the two subnets, which is formalized as follows: 
> $$M_{\text {diff }}=\operatorname{BINA}\left (\hat{Y}_{A}^{L}\right) \oplus \operatorname{BINA}\left (\hat{Y}_{B}^{L}\right)$$
> And then the masks can be used to find potential wrong prediction regions:
> $$\hat{Y}_{\text {diff }}^{L}=\operatorname{CLIP}\left (M_{\text {diff }}, \hat{Y}^{L}\right)$$
> Here, $\mathrm{CLIP} (\cdot)$ represents an operation to obtain the predictions corresponding to the masked areas. We design a rectification loss to guide the model to review these potentially mispredicted areas, the rectification loss is as follows:
> $$L_{r e c}=M S E\left (\hat{Y}_{\text {diff }}^{L}, Y_{\text {diff }}^{L}\right)$$
> Here $\mathrm{MSE} (\cdot)$ represents the Mean Squared Error (MSE) loss function, $Y_{\text {diff }}^{L}$ is the ground truth corresponding to these areas.

![[Mutual Correction Framework-Fig3.png]]

CDR 的过程如图 3 所示。CDR 的灵感来源于一个简单的事实：在二元分类场景中，如果两个分类器对于同一个像素有不同的预测，那么其中一个必定是错误的。因此，我们将不一致的预测视为可能的错误预测区域，并让网络审查这些区域。错误预测区域的掩码可以通过两个子网络的 softmax 输出 $\hat{Y}^{U}$ 之间的异或操作与二值化得到，形式化如下：

$$M_{\text {diff }}=\operatorname{BINA}\left (\hat{Y}_{A}^{L}\right) \oplus \operatorname{BINA}\left (\hat{Y}_{B}^{L}\right)$$

然后，这些掩码可以用于找到潜在的错误预测区域：

$$\hat{Y}_{\text {diff }}^{L}=\operatorname{CLIP}\left (M_{\text {diff }}, \hat{Y}^{L}\right)$$

这里，$\mathrm{CLIP}(\cdot)$ 表示一个用于获取与掩码区域相对应的预测的操作。
我们设计了一个矫正损失来引导模型审查这些可能被错误预测的区域，矫正损失如下：

$$L_{r e c}=M S E\left (\hat{Y}_{\text {diff }}^{L}, Y_{\text {diff }}^{L}\right)$$

这里，$\mathrm{MSE}(\cdot)$ 表示均方误差（MSE）损失函数，$Y_{\text {diff }}^{L}$ 是与这些区域相对应的真实值。

---

讲述了 CDR 的操作，其本质上是计算不同两个模型判断的不同的区域的值与真实值的偏差。

---

### DCPLG

$$
\begin{array}l
\text{Require}:\\
&\text{The set of labelled volumes for a batch}:  \left\{X^{L}, Y^{L}\right\} \\
&\text{The set of unlabelled samples for a batch}:  \left\{X^{U}\right\} \\
&\text{The subnet A}:  f_{A}(\cdot) \\
&\text{The subnet B}:  f_{B}(\cdot) \\
&\text{The Dice loss function}:  L_{\text {Dice }}(\cdot) \\
&\text{The batch size}:  b s \\
\text{Ensure}:\\
&\text{The pseudo labels of unlabeled samples for a batch},  Y_{p}^{U} \\
1:&  X \leftarrow\left\{X^{L}, X^{U}\right\}\\
2:&  T \leftarrow 0.1\\
3:& dice_{A} \leftarrow 0 ; \quad \operatorname{dice}_{B} \leftarrow 0\\
4:&  \hat{Y}_{A}^{L}, \hat{Y}_{A}^{U} \leftarrow \operatorname{softmax}\left (f_{A}(X)\right)\\
5:&  \hat{Y}_{B}^{L}, \hat{Y}_{B}^{U} \leftarrow \operatorname{softmax}\left (f_{B}(X)\right) \\
6:& \textbf{for }\text{each }  y_{i}^{L} \in Y^{L}  \text{ and }  \hat{y}_{A, i}^{L} \in \hat{Y}_{A}^{L}  \text{ and }  \hat{y}_{B, i}^{L} \in \hat{Y}_{B}^{L}  \textbf{do}\\
7:&  \quad  dice  _{A} \leftarrow  dice  _{A}+\frac{2}{b s} L_{\text {Dice }}\left (\hat{y}_{A, i}^{L}, y_{i}^{L}\right) \\
8:&  \quad  dice  _{B} \leftarrow  dice  _{B}+\frac{2}{b s} L_{\text {Dice }}\left (\hat{y}_{B, i}^{L}, y_{i}^{L}\right) \\
9:& \textbf{end for}\\
10:& \textbf{if } dice  _{A}<  dice  _{B}  \textbf{ then}\\
11:&  \quad P \leftarrow \hat{Y}_{A}^{U} \\
12:&  \quad Y_{p}^{U} \leftarrow \frac{P^{1 / T}}{P^{1 / T}+(1-P)^{1 / T}} \quad  \text{\# sharpening function}\\
13:& \textbf{else}\\
14:&  \quad P \leftarrow \hat{Y}_{B}^{U} \\
15:&  \quad Y_{p}^{U} \leftarrow \frac{P^{1 / T}}{P^{1 / T}+(1-P)^{1 / T}} \quad  \text{\# sharpening function}\\
16:& \textbf{end if}\\
17:& \textbf{return }  Y_{p}^{U}\\
\end{array}$$

---

**输入**：
- 一批数据集，包括标记的体积数据和对应的标签：$\left\{X^{L}, Y^{L}\right\}$
- 一批未标记的样本：$\left\{X^{U}\right\}$
- 两个子网络：$f_{A}(\cdot)$ 和 $f_{B}(\cdot)$，它们是神经网络的一部分，用于生成预测
- Dice 损失函数：$L_{\text {Dice }}(\cdot)$，用于计算两个概率分布之间的差异
- 批量大小：$bs$

**输出**：

- 未标记样本的伪标签：$Y_{p}^{U}$

**算法步骤**：

1. 将标记和未标记的样本合并为一个数据集 $X$。
2. 设置温度参数 $T$ 为 $0.1$。
3. 初始化两个 Dice 分数变量：$dice_{A}$ 和 $dice_{B}$，分别用于存储子网络 A 和 B 的 Dice 分数。
4. 使用子网络 A 和 B 对数据集 $X$ 进行预测，得到标记样本和未标记样本的预测概率分布 $\hat{Y}_{A}^{L}$、$\hat{Y}_{A}^{U}$、$\hat{Y}_{B}^{L}$ 和 $\hat{Y}_{B}^{U}$。
5. 进入循环，遍历每个标记样本 $y_{i}^{L}$ 以及对应的子网络 A 和 B 的预测 $\hat{y}_{A, i}^{L}$ 和 $\hat{y}_{B, i}^{L}$。
6. 在每次循环迭代中，计算子网络 A 和 B 的 Dice 分数，并将其累加到 $dice_{A}$ 和 $dice_{B}$ 中。Dice 分数衡量了预测与真实标签的相似性。
7. 结束循环。
8. 比较 $dice_{A}$ 和 $dice_{B}$ 的值，以确定哪个子网络的预测更好。如果 $dice_{A} < dice_{B}$，则选择子网络 A 的预测作为伪标签，否则选择子网络 B 的预测。
9. 使用所选的概率分布 $P$，通过一个称为 "sharpening function" 的函数来生成未标记样本的伪标签 $Y_{p}^{U}$。这个函数通过将概率分布的每个元素取 $1/T$ 次幂，并将其标准化，以获得伪标签。
10. 返回生成的未标记样本的伪标签 $Y_{p}^{U}$。

---

### Dynamic competitive pseudo label generation

> Algorithm 1 describes the pseudo code of our DCPLG module. We subtly use Dice loss to measure segmentation performance of subnets in real-time and select a better performing subnet as a pseudo-label generator for another subnet. Following the entropy minimization, we utilize the sharpening function to convert the network predictions into soft pseudo-labels. We use the dice loss as the evaluation criterion because the loss can directly reflect the dice coefficient and does not introduce additional computation, it is computed on labeled data. Therefore, DCPLG is almost free lunch that does not introduce additional network structures, and is easy to integrate into other semi-supervised methods. DCPLG can adopt other metrics for subnet performance evaluation, such as Hausdorff distance, average surface distance, etc.

**算法 1** 描述了我们的 DCPLG 模块的伪代码。我们巧妙地使用 Dice 损失来实时衡量子网络的分割性能，并选择性能更好的子网络作为另一个子网络的伪标签生成器。在熵最小化之后，我们利用锐化函数将网络预测转化为软伪标签。我们使用 Dice 损失作为评估标准，因为该损失可以直接反映 Dice 系数，不会引入额外的计算，它是在有标记数据上计算的。因此，DCPLG 几乎是一种零成本的方法，不会引入额外的网络结构，并且容易集成到其他半监督方法中。DCPLG 可以采用其他子网络性能评估的指标，如豪斯多夫距离、平均表面距离等。

---

解释了一下伪代码，本质上 DCPLG 就是就是 Dice 损失进行比大小。

---

### Overall loss function and model details

> The overall optimization loss function of one subnet can be formalized as follows:
> $$L_{\text {subnet }}=L_{s}+\lambda L_{u} \mathbb{I}(subnet \neq label\_generator)$$
> Where $L_{s}$ represents supervised loss, $L_{u}$ represents unsupervised loss and $\mathbb{I}(\cdot)$ is an indicator of whether the subnet is a pseudo-label generator. $\lambda$ is a weight that balances supervised and unsupervised losses.
> Supervised loss includes common segmentation loss and rectification loss $L_{r e c}$ derived from CDR. It can be expressed as follows:
> $$\begin{aligned} L_{s}  =\operatorname{Dice}\left (\hat{Y}^{L}, Y^{L}\right)+C E\left (\hat{Y}^{L}, Y^{L}\right) +\beta L_{\text {rec }}\left (\hat{Y}_{\text {diff }}^{L}, Y_{\text {diff }}^{L}\right) \end{aligned}$$
> Here, hyperparameters \beta is used to balance rectification loss and other losses. The unsupervised loss can be formulated as follows:
> $$L_{u}=\operatorname{MSE}\left (\hat{Y}^{U}, Y_{p}^{U}\right)$$
> Here, $Y_{p}^{U}$ is pseudo label.
> We adopt VNet as subnet A which is a popular choice in medical image segmentation. To implement inter-subnet mutual correcting, the performance gap of heterogeneous subnets should be slight. Therefore, the encoder of the VNet is replaced with a 3 D convolutional ResNet 34 as subnet B, called 3 D-ResVNet. During inference, we use the average of the outputs of the two subnets as the final prediction result. This framework is implemented by PyTorch with an NVIDIA V 100 GPU. And most of the parameter settings are consistent with the comparison methods. Specifically, the SGD optimizer is used to update the network parameters with weight decay 0.0001 , and momentum 0.9 . The initial learning rate is 0.01 and is divided by 10 after every 2500 iterations for a total of 6000 iterations. The batch size is 4 , which includes 2 labeled data volumes and 2 unlabeled volumes. Following Gaussian warming up function is used to control the weight $\lambda$ : $\lambda (t)=0.1 * e^{-5\left (1-t / t_{\max }\right)^{2}}$ . Where $t$ represents the current number of iterations, and $t_{\max }$ represents the total number of training iterations. $\beta$ is empirically set to 0.5 .

一个子网络的总体优化损失函数可以形式化如下：

$$L_{subnet}=L_{s}+\lambda L_{u} \mathbb{I}(subnet  \neq { label\_generator })$$

其中，$L_{s}$ 代表监督损失，$L_{u}$ 代表无监督损失，$\mathbb{I}(\cdot)$ 是子网络是否为伪标签生成器的指示器。λ 是一个权重，用于平衡监督和无监督损失。

监督损失包括常见的分割损失和由 CDR 导出的矫正损失 $L_{r e c}$，可以表示如下：

$$L_{s} = Dice (\hat{Y}^{L}, Y^{L}) + CE (\hat{Y}^{L}, Y^{L}) + \beta L_{\text {rec }}(\hat{Y}_{\text {diff }}^{L}, Y_{\text {diff }}^{L})$$

这里，超参数 $\beta$ 用于平衡矫正损失和其他损失。

无监督损失可以如下形式化：

$$L_{u}=MSE (\hat{Y}^{U}, Y_{p}^{U})$$

这里，$Y_{p}^{U}$ 是伪标签。

我们采用 VNet 作为子网 A，这是医学图像分割中的热门选择。要实现子网间相互纠错，异构子网的性能差距应该很小。因此，VNet 的编码器将替换为 3 D 卷积 ResNet 34 作为子网 B，称为 3 D-ResVNet。在推理过程中，我们使用两个子网输出的平均值作为最终预测结果。该框架由带有 NVIDIA V 100 GPU 的 PyTorch 实现。并且大多数参数设置与比较方法一致。具体来说，SGD 优化器用于更新权重衰减为 0.0001 和动量为 0.9 的网络参数。初始学习率为 0.01，每 2500 次迭代后除以 10，总共 6000 次迭代。批大小为 4 ，包括 2 个标记的数据卷和 2 个未标记的卷。我们采用高斯预热函数来控制权重 $\lambda (t)=0.1 * e^{-5\left (1-t / t_{\max }\right)^{2}}$ 。其中 $t$ 表示当前迭代次数，$t_{\max }$ 表示训练迭代总数。$\beta$ 根据经验设置为 0.5 。

---

**总体优化损失函数**：
一个子网络的总体优化损失函数由两部分组成，分别是监督损失和无监督损失。这个损失函数可以形式化表示为：

$$L_{subnet}=L_{s}+\lambda L_{u} \mathbb{I}(subnet  \neq { label\_generator })$$

- $L_{s}$ 代表监督损失，包括分割损失和由 CDR（可能是上下文中的方法）导出的矫正损失 $L_{r e c}$。
- $L_{u}$ 代表无监督损失，其中使用了伪标签。
- $\mathbb{I}(\cdot)$ 是指示器函数，表示子网络是否为伪标签生成器。
- $\lambda$ 是权重，用于平衡监督和无监督损失。

**监督损失**：

监督损失包括以下部分：

- Dice 损失（$Dice (\hat{Y}^{L}, Y^{L})$）：用于度量预测与真实标签的相似性。
- 交叉熵损失（$CE (\hat{Y}^{L}, Y^{L})$）：常用于分类任务的损失函数。
- 矫正损失（$L_{\text {rec }}(\hat{Y}_{\text {diff }}^{L}, Y_{\text {diff }}^{L})$）：通过一些方法（可能是 CDR）导出的矫正损失，其中超参数 $\beta$ 用于平衡此损失和其他损失。

**无监督损失**：

无监督损失采用均方误差（MSE）损失，用于衡量未标记样本的预测与伪标签之间的误差，即：

$$L_{u}=MSE (\hat{Y}^{U}, Y_{p}^{U})$$

**网络架构选择**：

作者选择了 VNet 作为子网 A，这是用于医学图像分割的常见选择。为了实现子网之间的相互纠错，作者还引入了一个异构子网 B，将 VNet 的编码器替换为 3 D 卷积 ResNet 34，形成 3 D-ResVNet。

**推理过程**：

在推理过程中，使用两个子网络输出的平均值作为最终预测结果，以提高模型性能。

**实现细节**：

- 使用 PyTorch 实现。
- 使用 SGD 优化器进行权重更新，包括权重衰减和动量。
- 使用学习率衰减策略，每 2500 次迭代后学习率除以 10，总共进行 6000 次迭代。
- 批量大小为 4，包括 2 个标记的数据卷和 2 个未标记的卷。
- 使用高斯预热函数来控制权重 $\lambda$。
- 超参数 $\beta$ 被设置为 0.5，用于平衡矫正损失和其他损失。

---

## Experiments

> Following the practice in the comparative literature, all methods (including MCF) are trained for 6 K fixed iterations to obtain the final model. To exclude the effect of dataset partitioning, we perform K-fold cross-validation and report the mean and standard deviation on two different modal medical datasets.

按照比较文献中的惯例，所有方法（包括 MCF）都经过了固定的 6,000 次迭代训练，以获得最终模型。为了排除数据集分割的影响，我们执行 K 折交叉验证，并报告在两个不同模态的医学数据集上的平均值和标准差。

### Datasets and Implementation Details

#### The Left Atrial Dataset (LA)

> The LA dataset includes 100 3 D gadolinium-enhanced MR imaging volumes with an isotropic resolution of $0.625 \times 0.625 \times 0.625 mm^3$ and the corresponding ground truth labels. We divide this dataset into 5 folds of 20 volumes each. For pre-processing, we first normalize all volumes to zero mean and unit variance, then crop each 3 D MRI volume with enlarged margins according to the targets. During training, the training volumes are randomly cropped to $112 \times 112 \times 80$ as the model input. During inference, a sliding window of the same size is used to obtain segmentation results with a stride of $18 \times 18 \times 4$.

左心房数据集包括 100 个 3 D 钆增强 MR 成像体积，其等间距分辨率为 $0.625\times 0.625\times 0.625 \mathrm{mm^3}$，并带有相应的地面真值标签。我们将这个数据集分成了 5 个包含 20 个体积的折叠。在预处理过程中，我们首先将所有体积归一化为零均值和单位方差，然后根据目标裁剪每个 3 D MRI 体积的边缘。在训练过程中，训练体积被随机裁剪为 $112\times 112\times 80$，作为模型的输入。在推断过程中，使用相同大小的滑动窗口以 $18\times 18\times 4$ 的步幅获取分割结果。

#### The NIH pancreas dataset

> A publicly available NIH Pancreas Dataset provides 82 contrast-enhanced abdominal 3 D CT volumes with manual annotation. The size of each CT volume is $512 \times 512 \times \mathrm{D}$ , where $\mathrm{D} \in[181,466]$ . We divide the NIH pancreas dataset into four folds, and the number of each fold is  20,20,21,21 , respectively. In preprocessing, like **Semi-supervised medical image segmentation through dualtask consistency** we use the soft tissue CT window of $[-120,240]\; \mathrm{HU}$ , and we crop the CT scans centering at the pancreas region, and enlarge margins with 25 voxels. The training volumes are randomly cropped to $96 \times 96 \times 96$ and the stride is $16 \times 16 \times 16$ at inference.

一个公开可用的 NIH 胰腺数据集提供了 82 个增强对比度的腹部 3 D CT 体积，并进行了手动标注。每个 CT 体积的尺寸为 $512 \times 512 \times \mathrm{D}$，其中 $\mathrm{D} \in [181,466]$。我们将 NIH 胰腺数据集分成了四个折叠，每个折叠的数量分别为 20、20、21 和 21。在预处理中，与 **Semi-supervised medical image segmentation through dualtask consistency** 类似，我们使用了 $[-120,240]\; \mathrm{HU}$ 的软组织 CT 窗口，并将 CT 扫描裁剪到以胰腺区域为中心，并扩大 25 个体素的边缘。训练体积被随机裁剪为 $96 \times 96 \times 96$，在推断时的步幅为 $16 \times 16 \times 16$。

#### Metrics

> We use four metrics to evaluate model performance, including regional sensitive metrics: Dice similarity coefficient (Dice), Jaccard similarity coefficient (Jaccard), and edge sensitive metrics: 95% Hausdorff Distance (95 HD) and Average Surface Distance (ASD).

我们使用四个指标来评估模型性能，包括区域敏感性指标：Dice 相似系数（Dice）、Jaccard 相似系数（Jaccard），以及边缘敏感性指标：95% Hausdorff 距离（95 HD）和平均表面距离（ASD）。

### Comparison on the LA dataset

![[Mutual Correction Framework-Fig4.png]]

![[Mutual Correction Framework-Tab1.png]]

> We first evaluate our proposed method on the left atrium segmentation task. The comparing methods include UAMT utilizing uncertainty-guided segmentation models, SASSNet that incorporates geometric constraints into the network, DTC that proposes multi-task consistency for medical image segmentation, and MC-Net for mutual consistency learning with cycle pseudo-labels. In addition, we also implement the MT based UA-MT for a more comprehensive comparison. The five-fold cross-validation results under 20% labeled data training are presented in Tab. 1. In addition, the metrics of VNet and 3 DResVNet at 100% and 20% labeled data are reported as reference performance upper bound and baselines. As can be seen from the Tab. 1, all methods benefit from unlabeled data, but MT has the least gain and the worst stable performance with the largest standard deviation. UA-MT outperforms the MT method, illustrating that the uncertainty map can improve the performance of the student model. Compared with other existing methods, MC-Net achieves the best results on Dice and Jaccard metrics with stable performance. While SASSNet outperforms other comparison methods on 95 HD and ASD, showing that shape priors improve edge segmentation. Notably, the MCF framework outperforms the SOTA method on all metrics, especially on the edge-sensitive metrics 95 HD and ASD. Compared with SSANet, 95 HD drops from 9.02 to 6.32, ASD drops from 2.40 to 1.90, and the performance is more stable. Fig. 4 shows the visualization results of MCF and comparison methods on left atrial segmentation. Compared with other methods, MCF has a higher overlap rate with labels and produces fewer false segmentations with more details.

首先，我们在左心房分割任务上评估了我们提出的方法。比较方法包括利用不确定性引导分割模型的 UAMT、将几何约束纳入网络的 SASSNet、为医学图像分割提出多任务一致性的 DTC，以及使用循环伪标签进行相互一致性学习的 MC-Net。此外，我们还实现了基于 MT 的 UA-MT，以进行更全面的比较。在使用 20%标记数据进行五折交叉验证的结果如表 1 所示。此外，VNet 和 3 DResVNet 在 100%和 20%标记数据下的指标也报告为参考性能上限和基准线。从表 1 可以看出，所有方法都受益于未标记数据，但 MT 的增益最小，且稳定性最差，标准差最大。UA-MT 优于 MT 方法，说明不确定性图可以提高学生模型的性能。与其他现有方法相比，MC-Net 在 Dice 和 Jaccard 指标上取得了最佳结果，并具有稳定的性能。而 SASSNet 在 95 HD 和 ASD 上优于其他比较方法，显示出形状先验改善了边缘分割。值得注意的是，MCF 框架在所有指标上均优于 SOTA 方法，特别是在对边缘敏感的指标 95 HD 和 ASD 上。与 SSANet 相比，95 HD 从 9.02 下降到 6.32，ASD 从 2.40 下降到 1.90，并且性能更稳定。图 4 显示了 MCF 和比较方法在左心房分割上的可视化结果。与其他方法相比，MCF 与标签具有更高的重叠率，生成更多细节的虚假分割。

### Comparison on the pancreas dataset

![[Mutual Correction Framework-Tab2.png]]

![[Mutual Correction Framework-Fig5.png]]

> The pancreas is located deep in the abdomen and varies considerably in size, location, and shape. In addition, pancreatic CT volumes have a more complex background compared to left atrial MRI volumes. Therefore, pancreas segmentation is more challenging than left atrial segmentation. Based on this, we conduct experiments on the pancreas dataset to further evaluate our proposed method. As shown in Tab. 2, we report the 4-fold cross-validation results under 12 labeled data and 50 unlabeled data. It can be seen that the segmentation metrics of all methods are worse than the left atrium segmentation, demonstrating the challenge of semi-supervised pancreas segmentation. Like left atrium segmentation, VNet outperforms 3 D-ResNet in fully supervised settings, but 3 D-ResVNet performs better overall with fewer labeled training samples. MT outperforms other comparison methods in Dice and Jaccard metrics, while DTC and SASSNet win at 95 HD and ASD, respectively. What is more interesting is that the performance of these comparison methods on the two databases is not consistent, it seems that the method that performs poorly on LA segmentation shows an advantage on pancreas segmentation, such MT. Overall, the performance gap between the compared methods is not large. This shows the complexity of pancreas segmentation and the variability between different medical image segmentation tasks. We think this may be related to data processing, dataset size, volumetric properties, and method applicability. However, this also shows that our method has stronger robustness across datasets. Notably, the MCF framework outperforms the SOTA method on all metrics, especially the 95 HD drop of 1.61. Fig. 5 shows the visual segmentation results of these methods. Compared with other comparison methods, MCF obtains more accurate segmentation with a smoother and clearer edge. The other comparison methods are prone to discrete mispredictions and small protrusions or depressions in the edges.

胰腺位于腹部深处，大小、位置和形状各异。此外，与左心房 MRI 体积相比，胰腺 CT 体积具有更复杂的背景。因此，胰腺分割比左心房分割更具挑战性。基于此，我们在胰腺数据集上进行实验，以进一步评估我们提出的方法。如表 2 所示，我们报告了在 12 个标记数据和 50 个未标记数据下的 4 折交叉验证结果。可以看出，所有方法的分割指标均不如左心房分割，表明半监督胰腺分割的挑战性。与左心房分割类似，VNet 在完全监督设置下优于 3 D-ResNet，但在较少标记训练样本的情况下，3 D-ResVNet 的性能更好。MT 在 Dice 和 Jaccard 指标上优于其他比较方法，而 DTC 和 SASSNet 在 95 HD 和 ASD 上获胜。更有趣的是，这些比较方法在两个数据库上的性能不一致，似乎在 LA 分割上性能差的方法在胰腺分割上具有优势，例如 MT。总体而言，比较方法之间的性能差距不大。这显示了胰腺分割的复杂性以及不同医学图像分割任务之间的变异性。我们认为这可能与数据处理、数据集大小、体积属性和方法适用性有关。然而，这也表明我们的方法在跨数据集上具有更强的稳健性。值得注意的是，MCF 框架在所有指标上均优于 SOTA 方法，尤其是 95 HD 降低了 1.61。图 5 显示了这些方法的可视化分割结果。与其他比较方法相比，MCF 获得了更准确的分割，边缘更加平滑和清晰。其他比较方法容易出现离散的错误预测以及边缘上的小突起或凹陷。

### Analysis and Ablation

#### CDR and bias correction

![[Mutual Correction Framework-Tab3.png]]

![[Mutual Correction Framework-Fig6.png]]

> The purpose of CDR is to use prediction discrepancies to guide the network to correct its own mistakes. A simple and effective experiment is used to verify the effectiveness of CDR: We train two baseline networks (i.e., VNet and 3 D-ResVNet) with and without CDR on the LA dataset and show the single network performance in Tab. 3. Note that V and R in this table represent VNet and 3 D-ResVNet, respectively. We can see that the performances of the two baselines without CDR are similar. CDR brings significant and consistent improvement to the baseline networks in all metrics, especially 95 HD: VNet drops 5.83 points and 3 D-ResVNet drops 4.13 points. This is because the bias pixels are mainly located on the edge of the object, like shown in Fig. 1 (d). Regarding the region-sensitive metrics (Dice and Jaccard), both baselines improved by about 2 points after adding CDR. Although VNet with CDR has the smallest improvement in ASD, it is also close to 1 point. In general, VNets benefit more from CDR. The segmentation visualization results are shown in Fig. 6. Red and blue represent the results of VNet and 3 D-ResVNet, respectively. First and second rows represent w/ or w/o CDR, respectively. It can be clearly found that there are some wrong predictions that always exist during the training process of these baseline networks, and CDR helps the network correct these errors. This confirms our hypothesis that although the network has a strong learning ability, they easily fall into their own biases. Moreover, CDR reduces out-of-body discrete errors and makes edges clearer.

CDR 的目的是利用预测差异来引导网络纠正自己的错误。我们进行了一项简单而有效的实验，以验证 CDR 的有效性：我们在 LA 数据集上训练了两个基线网络（即 VNet 和 3 D-ResVNet），分别使用 CDR 和不使用 CDR，并在表 3 中展示了单个网络的性能。请注意，表中的 V 和 R 分别代表 VNet 和 3 D-ResVNet。我们可以看到，没有 CDR 的两个基线的性能相似。CDR 在所有指标上为基线网络带来了显著和一致的改进，特别是在 95 HD 方面：VNet 降低了 5.83 个点，3 D-ResVNet 降低了 4.13 个点。这是因为偏差像素主要位于物体的边缘，如图 1（d）所示。关于区域敏感的指标（Dice 和 Jaccard），在添加 CDR 后，两个基线都提高了约 2 个点。尽管具有 CDR 的 VNet 在 ASD 方面的改进最小，但也接近 1 个点。总的来说，VNets 更多地受益于 CDR。分割可视化结果如图 6 所示。红色和蓝色分别代表 VNet 和 3 D-ResVNet 的结果。第一和第二行分别表示 w/或 w/o CDR。可以清楚地看到，在这些基线网络的训练过程中总是存在一些错误的预测，而 CDR 有助于网络纠正这些错误。这证实了我们的假设，即尽管网络具有很强的学习能力，但它们很容易陷入自己的偏见。此外，CDR 减少了离体离散错误，并使边缘更清晰。

#### DCPLG and consistency

![[Mutual Correction Framework-Fig7.png]]

> To show the performance changes during training for both consistency regularization and DCPLG, we replace DCPLG in MCF with consistency regularization i.e., encourage subnets to have the same predictions, and remove other redundant components to avoid superfluous influence. Fig. 7 shows the dynamic changes in the performance of the model on the LA dataset with 20% labeled data under these two settings. An interesting finding is that all metrics of consistency regularization decrease to varying degrees with increasing training steps. Specifically, before 2 K iterations, the consistency regularization outperforms DCPLG, but after 2 K iterations, the situation reverses. In subsequent training, the gap gradually widens, especially in Dice, Jaccard, and 95 HD. And after 5 K iterations, both methods show performance degradation, but DCPLG is slight.

为了展示一致性正则化和 DCPLG 在训练过程中的性能变化，我们在 MCF 中将 DCPLG 替换为一致性正则化，即鼓励子网络具有相同的预测，并删除其他多余的组件以避免不必要的影响。图 7 展示了在这两种设置下，模型在具有 20%标记数据的 LA 数据集上性能的动态变化。一个有趣的发现是，随着训练步骤的增加，所有一致性正则化的指标都会不同程度地下降。具体来说，在 2 K 次迭代之前，一致性正则化的性能优于 DCPLG，但在 2 K 次迭代之后，情况发生了逆转。在随后的训练中，差距逐渐扩大，特别是在 Dice、Jaccard 和 95 HD 方面。在经过 5 K 次迭代之后，两种方法都显示出性能下降，但 DCPLG 的下降幅度较小。

#### Effects of different components

> Ablation experiments are performed to demonstrate the effectiveness of MCF, and the results are presented in Tab. 3. First, since the predicted results of MCF are obtained by averaging the results of the two subnets, we verify the performance when integrating VNet and 3 D-ResNet with the averaging operation, i.e. Vm-R in the Tab. 3. The performance of the simple average model is improved, but it is weaker than the V/R+CDR. V/R+CDR means that the model is trained by V+R+CDR and then tested subnets separately, Setting V/R+DCPLG is similar. Compared with V-m-R, V+R+CDR achieves gains of 1.68, 2.27, 3.41, and 0.72 on Dice, Jaccard, 95 HD, and ASD, respectively. While the gains of V+R+DCPLG are 3.6, 5.02, 4.57 and 0.84, indicating that DCPLG helps the model learn from unlabeled data. In the end, the complete MCF model achieved the best results.

进行消融实验以展示 MCF 的有效性，并将结果呈现在表格 3 中。首先，由于 MCF 的预测结果是通过对两个子网络的结果进行平均得到的，我们验证了在整合 VNet 和 3 D-ResNet 时执行平均操作时的性能，即在表格 3 中的 V/R 模型。简单平均模型的性能得到了改善，但仍然比 V/R+CDR 模型要弱。V/R+CDR 表示模型是通过 V+R+CDR 进行训练，然后对子网络进行单独测试的，设置 V/R+DCPLG 类似。与 V-m-R 相比，V+R+CDR 在 Dice、Jaccard、95 HD 和 ASD 方面分别获得了 1.68、2.27、3.41 和 0.72 的增益。而 V+R+DCPLG 的增益分别为 3.6、5.02、4.57 和 0.84，表明 DCPLG 有助于模型从未标记的数据中学习。最终，完整的 MCF 模型取得了最佳结果。

#### Ablation for rectification loss

![[Mutual Correction Framework-Tab4.png]]

> The discrepancy prediction regions between subnets are very small and scattered, which are not suitable for implementing Dice loss, these predictions are obtained under the guidance of CE loss, so a common other loss i.e. MSE is adopted. Tab. 4 reports the segmentation performance of the model when CE and MSE are used as rectification losses, respectively. Compared with CE, MSE achieves better segmentation results, so we adopt MSE as the correction loss.

子网络之间的差异性预测区域非常小且分散，不适合使用 Dice 损失来实现，这些预测是在 CE 损失的指导下获得的，因此采用了一种常见的其他损失，即 MSE。表格 4 报告了在使用 CE 和 MSE 作为矫正损失时模型的分割性能。与 CE 相比，MSE 实现了更好的分割结果，因此我们采用 MSE 作为矫正损失。

#### Ablation for hyperparamerters β

![[Mutual Correction Framework-Tab5.png]]

> We find that the model is not very sensitive to the hyperparameter β, and Tab. 5 shows the metrics when β takes 0.3-0.7. According to this empirical result, β is set to 0.5 in this work.

我们发现模型对超参数 β 不太敏感，表 5 显示了当 β 取 0.3-0.7 时的指标。根据这一经验结果，在本工作中将 β 设置为 0.5。

---

讲述了一些测试的结果。

---

## Discussions and Conclusion

> In this paper, we propose a new framework called MCF for semi-supervised medical image segmentation, which enables the network to be aware of its own mistakes and perform bias correction through inter-subnet comparisons. To unleash the potential of the dual-subnet architecture, MCF introduces two different subnets that update parameters independently. The CDR takes the difference predictions of the subnets as potential bias areas and guides the network to review and correct them. This is almost a free lunch and can be easily integrated into other semi-supervised or fully-supervised methods. The DCPLG is essentially like a mock exam that students take before their final exams. Combined with the characteristics of medical image segmentation datasets (i.e., all samples are related to the target), DCPLG is used to dynamically select pseudo-label generators to improve the quality of pseudo-labels. Inheriting the idea of DCPLG to modify and apply it to natural image processing is our further work. Finally, segmentation results on two public benchmark datasets with different modalities demonstrate the potential of MCF on semi-supervised medical images, which achieves state-of-the-art performance.

在本文中，我们提出了一个名为 MCF 的新框架，用于半监督医学图像分割，它使网络能够意识到自己的错误，并通过子网络之间的比较进行偏差校正。为了发挥双子网络架构的潜力，MCF 引入了两个不同的子网络，它们独立地更新参数。CDR 将子网络的差异预测视为潜在的偏差区域，并引导网络对其进行审查和校正。这几乎是一种免费午餐，可以轻松地集成到其他半监督或完全监督的方法中。DCPLG 本质上类似于学生在期末考试之前参加的模拟考试。结合医学图像分割数据集的特点（即所有样本都与目标相关），DCPLG 用于动态选择伪标签生成器，以提高伪标签的质量。将 DCPLG 的思想继承并应用于自然图像处理是我们的进一步工作。最后，对两个不同模态的公共基准数据集上的分割结果展示了 MCF 在半监督医学图像上的潜力，它实现了最先进的性能。

## Acknowledgements

> This work was supported in part by the National Key Research and Development Project under Grant 2019 YFE 0110800, in part by the National Natural Science Foundation of China under Grant 62172067 and 61976031, in part by the National Major Scientific Research Instrument Development Project of China under Grant 62027827, in part by Chongqing University of Posts and Telecommunications Ph. D. Innovative Talents Project under Grant BYJS 202216.

这项工作得到了以下部分资助：国家重点研发计划项目，授权号 `2019 YFE 0110800` 的支持；中国国家自然科学基金，授权号 `62172067` 和 `61976031` 的支持；中国国家重大科学研究仪器研发项目，授权号 `62027827` 的支持；以及重庆邮电大学博士创新人才项目，授权号 `BYJS 202216` 的支持。

# 代码阅读

## 代码结构

```txt
├── code
│   ├── dataloaders
│   │   ├── __init__. py
│   │   ├── la_heart_processing. py
│   │   ├── la_heart.py
│   │   └── utils.py
│   ├── networks
│   │   ├── ResNet34.py
│   │   ├── resnet.py
│   │   └── vnet.py
│   ├── test_LA_MCF.py
│   ├── test_util.py
│   ├── train_MCF.py
│   └── utils
│       ├── __init__.py
│       ├── losses.py
│       ├── opt_utils.py
│       ├── ramps.py
│       ├── ssim.py
│       └── util.py
├── dataset
│   ├── LA
│   │   ├── Flods
│   │   └── LA_data
│   └── Pancreas
│       ├── Flods
│       └── pancreas_data
├── LICENSE
└── README.md
```
## Dataloaders

### `la_heart_processing.py`

将医学图像数据从 NRRD 文件格式转换为 H 5 文件格式。

### `la_heart.py`

#### LAHeart 类

`LAHeart` 类是一个自定义的 PyTorch 数据集类，用于加载和处理心脏图像数据。

- `__init__` 方法初始化数据集，接受以下参数：
    - `base_dir`：数据集的基本目录路径。
    - `split`：数据集的拆分（训练、验证或测试）。
    - `train_flod`：训练折叠的文件名。
    - `common_transform`：用于通用数据转换的函数。
    - `sp_transform`：用于特定数据转换的函数。
- `__len__` 方法返回数据集的样本数量。
- `__getitem__` 方法用于获取数据集中的单个样本。

#### 数据处理函数

`CenterCrop`、`RandomCrop`、`RandomRotFlip`、`RandomNoise`、`CreateOnehotLabel`、`GaussianBlur` 和 `ToTensor` 是一些用于数据预处理和转换的函数。它们可以对输入的图像和标签进行裁剪、翻转、添加噪声、生成独热编码标签以及将数据转换为 PyTorch 张量、用于对图像应用高斯模糊。

#### 采样器

`TwoStreamBatchSampler` 类是一个自定义的采样器类，用于实现两个不同数据流的采样。

- 这个采样器接受两组索引集合，分别对应两个数据流。
- `primary_batch_size` 是主要数据流的批次大小，而 `secondary_batch_size` 是次要数据流的批次大小。
- 通过迭代两个数据流的索引，它能够生成联合批次，其中包含主要数据流和次要数据流的样本。

### `utils.py`

- `recursive_glob`: 搜索指定目录下的所有文件，找到文件名以指定后缀结尾的文件，并返回它们的路径列表。
- `get_cityscapes_labels` 和 `get_pascal_labels`: 这两个函数返回用于不同数据集（Cityscapes 和 PASCAL VOC）的标签颜色映射，将颜色映射到类别。
- `encode_segmap`: 将分割标签图像编码成类别索引图像，其中每个像素的值表示其所属类别的索引。
- `decode_seg_map_sequence` 和 `decode_segmap`: 这些函数用于将编码后的分割标签图像解码成彩色图像，以便可视化分割结果。
- `generate_param_report`: 用于生成参数报告并将其写入指定的日志文件中。
- `cross_entropy2d`: 计算分割模型输出的交叉熵损失。
- `lr_poly`: 根据迭代次数调整学习率的函数。它使用多项式衰减函数来降低学习率。
- `get_iou` 和 `get_dice`: 用于计算分割模型的 IoU（交并比）和 Dice 系数。
- `get_mc_dice`: 用于计算多类别的 Dice 系数。

## Networks

### `resnet.py`

定义了一个通用的三维残差网络。

### `ResNet34.py`

定义了一个三维的 ResNet 34 网络。

### `vnet.py`

定义了一个 VNet 网络。

## Utils

### `losses.py`

实现了一些计算损失函数的函数

### `opt_utils.py`

- `partition(image, div_num)`：分割图像并重新排列
- `cut_partition(image, div_num)`：对一部分进行切割操作
- `Decomposition_and_reorganization_MRI (image, div_num)`：调用 partition 函数来对每幅图像进行分割和重新组织，返回一个包含重新排列的图像块的列表。
- `Cutout_MRI(image, div_num)`：此函数返回处理后的图像、原始被切割的块以及切割的坐标信息。
- `ToTensor (sample)`：将其中的图像数据从 NumPy 数组转换为 PyTorch 张量。

### `ramps.py`

包含用于根据当前的训练步骤或周期以及过渡期的长度来调整超参数的函数。

### `ssim.py`

定义了一些用于计算图像结构相似性（SSIM）和多尺度图像结构相似性（MS-SSIM）的函数和模块。

### `util.py`

包含加载模型、自定义数据采样、记录训练日志以及学习率衰减的类与函数。

## `train_MCF.py`

代码中先进行初始设置，其中需要注意的是将 `root_path` 参数修改为自己的数据路经（如本人使用 `LA_data`，则设置为 `/home/axi/YCode/MCF/dataset/LA/LA_data`）。

其次创建两个模型，分别为 `ResNet34` 与 `VNet`，并使用 `LAHeart` 加载数据。

接下来进入循环进行训练：

- 计算 `VNet` 和 `ResNet34` 模型的输出。
- 计算监督损失，包括交叉熵损失和 `Dice` 损失。
- 通过 `Dice` 损失计算 `Good_student` 对应模型。
- 根据 `Good_student` 变量选择学生模型（`VNet` 或 `ResNet34`），并计算一致性损失。
- 根据一致性权重和损失计算总损失。
- 执行反向传播和权重更新。
- 记录损失和其他指标，以供监视和可视化。

结束训练并保存模型。

# 总结

个人感觉，MCF 模型的特点在于说，不同于之前的 MT 的思想，使用一个模型指导另一个模型（即提供标注），而是将教师与学生的身份进行动态切换。其大多数的模型中的内容设置相当朴素（如对于各种参数的设置以及选取（当然也可能设计了很多，而我没有发现），以及在阅读代码的时候，发现甚至 MCF 都不是一个模型，而是分成两个模型，其思想仅在 epoch 训练的过程中体现），但在如此情况下依然能具有 SOTA 表现，意味着这种动态提供伪标签的思想是很有可行性的，若在此基础之上进行拓展，或许可以保留基础的动态切换的思想，而对于其他的内容进行适当修改。

# 附录

此处主要包含一些名词的解释，本人第一次接触相关领域，不少的名词也是第一次见到，于是进行了查询与了解，将其与一些我了解的名词一起放到这里。

## CT 和 MRI

CT（计算机断层扫描）和 MRI（磁共振成像）是两种常用于医学影像的不同成像技术，用于诊断和疾病监测。

## EMA

指数移动平均法（Exponential Moving Average，EMA）是一种用于数据平滑和趋势分析的统计方法，其在计算平均值时引入了指数权重，使得最新数据点具有更高的权重，从而更灵敏地反映数据的变化趋势。

EMA 之所以有效，是因为其公式：

$$
v_{t}=\beta \cdot v_{t-1}+(1-\beta) \cdot \theta_{t}
$$

其中在深度学习的优化过程中，$\theta_t$ 是 t 时刻的模型权重 weights，$v_t$ 是 t 时刻的影子权重（shadow weights）。在梯度下降的过程中，会一直维护着这个影子权重，但是这个影子权重并不会参与训练。

由此展开，可以得到：

令第 n 时刻的模型权重（weights）为 $v_{n}$，梯度为 $g_{n}$，可得:

$$\begin{aligned}
\theta_{n} & =\theta_{n-1}-g_{n-1} \\
& =\theta_{n-2}-g_{n-1}-g_{n-2} \\
& =\ldots \\
& =\theta_{1}-\sum_{i=1}^{n-1} g_{i}
\end{aligned}$$

令第 n 时刻 EMA 的影子权重为 $v_{n}$，可得：

$$\begin{aligned}
V_{n} & =\alpha v_{n-1}+(1-\alpha) \theta_{n} \\
& =\alpha\left (\alpha v_{n-2}+(1-\alpha) \theta_{n-1}\right)+(1-\alpha) \theta_{n} \\
& =\ldots \\
& =\alpha^{n} v_{0}+(1-\alpha)\left (\theta_{n}+\alpha \theta_{n-1}+\alpha^{2} \theta_{n-2}+\ldots+\alpha^{n-1} \theta_{1}\right)
\end{aligned}$$

代入上面 $\theta_{n}$ 的表达, 令 $v_{0}=\theta_{1}$ 展开上面的公式，可得：

$$\begin{aligned}
V_{n}&=\alpha^{n} v_{0}+(1-\alpha)\left (\theta_{n}+\alpha \theta_{n-1}\right.  \left.+\alpha^{2} \theta_{n-2}+\ldots+\alpha^{n-1} \theta_{1}\right) \\
&=\alpha^{n} v_{0}+(1-\alpha)\left (\theta_{1}-\sum_{i=1}^{n-1} g_{i}\right. +\alpha\left (\theta_{1}-\sum_{i=1}^{n-2} g_{i}\right)+\ldots\\
&+\alpha^{n-2}\left (\theta_{1}-\sum_{i=1}^{1} g_{i}\right) \left.\quad+\alpha^{n-1} \theta_{1}\right) \\
&= \alpha^{n} v_{0}+(1-\alpha)\left (\frac{1-\alpha^{n}}{1-\alpha} \theta_{1}-\sum_{i=1}^{n-1} \frac{1-\alpha^{n-i}}{1-\alpha} g_{i}\right) \\
&= \alpha^{n} v_{0}+\left (1-\alpha^{n}\right) \theta_{1}-\sum_{i=1}^{n-1}\left (1-\alpha^{n-i}\right) g_{i} \\
&= \theta_{1}-\sum^{n-1}\left (1-\alpha^{n-i}\right) g_{i}
\end{aligned}$$

其本质上是一个 learning rate decay。

资料来源： https://zhuanlan.zhihu.com/p/68748778

本文中，MT 中的 Teacher 通过 Student 的权重，使用 EMA 实现。

## Dice 损失

$$
\text { DiceLoss }=1-\frac{2|X \bigcap Y|+\text { smooth }}{|X|+|Y|+\text { smooth }}
$$

其中 smooth 防止分母为 0。

## CE 与 MSE

交叉熵与均方损失，不解释。

$$CE (y, \hat{y}) = - \sum_{i=1}^{N} y_i \log (\hat{y}_i)$$

$$MSE (y, \hat{y}) = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2$$

## Sharpening function

$$
\text { Sharpen }(p, T)_{i}:=p_{i}^{\frac{1}{T}} / \sum_{j=1}^{L} p_{j}^{\frac{1}{T}}
$$

其作用是锐化或者平缓熵，$T$ 越大，熵越大，反之变小。