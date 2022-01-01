---
layout: post
title: Unsupervised Representation Learning With Deep Convolutional Generative Adversarial Networks (2016)
categories: [DeepLearning]
tags: [Unsupervied, vision, GAN, DCGAN]
fullview: true
comments: true
---

### overview

```
Before discourse about the paper. we need to know what terms used in paper means. So for all post in this category, I'll check the meaning of the words first. Then write about the technology.
```

The purpose of this paper is propose novel way to learn general image feature to utilize for other tasks(mostly in supervised learning.). This paper suggest a GAN model to extract the representation. 

### Terms

- pretext task : task used for learning representation in transfer learning. In transfer learning process the representation is used for other tasks like detecton or classification.
- expoit : to utilize. (I knew that word is for abusing)
- chromatic aberration : Wrong focus makes each color channel shifts a little. light raies that have different frequency has different refractive index. If a ray pass through the lens, lens became a prism. To prevent that, typical camera has lots of lens and to move them to adjust the refract. (In korean 색수차)

### my abstract

1. CNNs are widly used for supervised vision tasks.
2. Despite the popularity, CNNs for unsupervised learning are not favored.
3. The paper suggest GAN model consist of Convolution layers, which can learn hierarchy of representation both on Generator and discriminator.
4. Not done. Still working.

