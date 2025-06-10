---
title: Research Project - Tracking Trend Changes in Streaming Tensor Using AutoEncoder
layout: single
---
<iframe src="https://1drv.ms/p/s!AuLEAGq4CoXh20B5jlyUJrOZjRPE?embed=1&amp;em=2&amp;wdAr=1.3333333333333333" width="476px" height="481px" frameborder="0">This is an embedded <a target="_blank" href="https://office.com">Microsoft Office</a> presentation, powered by <a target="_blank" href="https://office.com/webapps">Office</a>.</iframe>

*This post is a review of research project led and conducted by me regarding tracking trend changes in streaming tensor data using autoencoder*

*#Autoencoder #DeepLearning # TensorDecomposition #ConceptDrift #TrendDetection #tSNE #HighDimensionalDataAnalysis* #PCA #DimensionReduction 

Tensor is a multi-dimensional array that can be useful for storing data with variety of features. However, as the size and dimension of a tensor grows, the harder it becomes to interpret and extract meaningful information from the noisy bulk of data. To address this issue, many researches are being done to track trend changes in tensors. This post will introduce a new attempt to captures trend changes in tensors using autoencoder.

Autoencoder is a type of neural network trained to copy its input to its output. In detail, the encoder network of autoencoder encodes the given input to a lower dimensional feature vector (although does not always have be a vector). During this process, encoder learns to compress the input so that the encoded vector only contains important information. The decoder network, then, takes the encoded vector as its input and tries to reconstruct the original input of autoencoder. Through this encoding and decoding process, the autoencoder network learns to extract the essence of the input data. The proposed method for theme tracking is based on this very ability of autoencoder.

![image info](../assets/images/autoencoder-architecture.png)


To capture theme changes in online setting, we must analyze each incoming tensor batch and check if it has changed in any way from earlier batches. To determine that, we train autoencoder so that it compresses the incoming tensor batch into a smaller latent structure that  represents the target batch in a compact manner. Once the network is trained, we pass each incoming tensor batch into the encoder network and gain corresponding latent structures. Then, we map the latent structure with a relatively high dimension to low dimension, 2 dimension in this post. Mapping is done via T-SNE method. The following figure shows the encoded tensor batches getting mapped to two dimensional coordinate.

![image info](../assets/images/aevec.PNG)

To test the method, the author used a video that has several distinct theme change in each section. The video is shown below. The result was that the encoded structures of each section were mapped nearby and as the section changed gradually, the location of the mapped structures moved from one cluster to another. This shows that this method is effective in tracking theme changes in streaming tensor. Possible improvements of this method would be to reduce memory usage and update T-SNE so that mapping can occur in online setting as well.

The figure below compares the expected trend changing scene and what's detected by the proposed method. The left three screenshots marks the change of the scene from the video attached below. This is where old trend (old scene) ends and new trend (new scene) begins and the change occurs gradually as the video shown below. The right figure shows the frame of the points on T-SNE plot that began to drift away from clusters, indicating the start of a new trend.

![image info](../assets/images/change.PNG)


This is a T-SNE plot showing the changes of frames in the video. Each section is marked in different color. As you can see, blue and green dots are clustered well. Orange dots, however, seem to trail from blue dots to green dots. This makes sense since orange dots represent the middle section of the video where section change occurs both in the beginning and in the end.

![image info](../assets/images/res.PNG)
