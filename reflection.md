Task 1:
First conflicting result came when ViT showed supposed translation equivariance in Translation test. Realised this was due to its pretraining on ImageNet and self-attention. This highlighted that biases can be learned, not just built-in. The ViT's robustness wasn't an architectural feature but a byproduct of its extensive pre-training with data augmentations like random cropping.

Secondly, ViT performed horrendously on Sketch (OOD) in Domain Generalisation when it was supposed to outperform the ResNet easily (source: SPROJ). The ViT's architecture allows it to learn global, shape-based relationships, but it needs a massive dataset to do so effectively. Hence, on PACS, it failed to learn a robust representation and defaulted to simplistic heuristics, as seen in its confusion matrix

Task 2:

Our GAN showed no signs of mode collapse, maintaining balanced class coverage (5.4-19.5%) across all CIFAR-10 categories, while the VAE exhibited severe class imbalance with 41.4% of reconstructions classified as cats. This class imbalance can be attributed to misclassifications of the blurry quality of the VAE reconstructions though. This contradicts the common assumption that GANs suffer from poor diversity while VAEs provide comprehensive coverage.

The VAE's counterintuitive OOD behavior was equally surprising - achieving lower reconstruction error on SVHN digits (0.0066) than on CIFAR-10 training data (0.0230). This suggests the complexity mismatch between datasets matters more than distributional familiarity. This shows how we can not depend on reconstruction alone for anomaly detection.

Our latent space analysis revealed minimal semantic organization in the VAE despite using β=0.5 for disentanglement. The PCA visualization showed overlapping clusters with no clear class boundaries, and latent traversal experiments yielded negligible semantic variation. This emphasizes how dataset complexity (32×32 CIFAR-10) can limit disentanglement, regardless of architectural choices.

Task 3:

We were struck by how well CLIP held up on heavily corrupted images. Unlike CNNs, which quickly lose confidence under noise, CLIP maintained both accuracy and stability. This highlighted just how differently its features are extracted compared to standard convolutional models.

That said, our analysis had clear limitations. We only compared against a single baseline (ResNet-50) and worked with a single dataset (CIFAR-10). The low resolution of CIFAR-10 (32×32) is far from ideal for CLIP, which was pre-trained on higher-resolution web images. We also did not explore some of CLIP’s known weaknesses, such as its societal biases from internet data or its struggles with fine-grained reasoning tasks.

Even so, our results are consistent with prior literature. Geirhos et al. (2019) showed CNNs’ strong texture bias, which our cue-conflict test replicated. Likewise, CLIP’s robustness and zero-shot performance mirrored the findings of Radford et al. (2021). In that sense, our study offered a small-scale but practical confirmation of these broader insights.