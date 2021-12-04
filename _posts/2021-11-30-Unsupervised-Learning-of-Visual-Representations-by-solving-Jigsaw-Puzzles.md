---
layout: post
title: Unsupervised Learning of Visual Representations by Solving Jigsaw Puzzles
categories: [DeepLearning]
tags: [Unsupervied, vision]
fullview: true
comments: true
---

### overview

```
Before discourse about the paper. we need to know what terms used in paper means. So for all post in this category, I'll check the meaning of the words first. Then write about the technology.
```

The purpose of this paper is proposing novel method to train a network with unsupervised(self-supervised) way for using in tranfer learning (AlexNet Compatitive)

### my abstraction

1. The paper trying to train a network used for transfer learning to AlexNet
2. The paper trying to train a network with unsupervised(self-supervised) way.
3. The Purpose of the unsupervised learning is to learn representation of input image WELL enough to used that representation in transfer learning(fine fitting).
4. Solving a Jigsaw puzzle is great way to make a network learn representation WELL.
5. Because solving jigsaw puzzle require high-level representation on image (not low-level feature like color and texture). It makes using that representation for general purpose easy.
6. In jigsaw puzzle, orientation of pieces is related to all pieces. We can not find out that with seeing just 2 pieces.
7. So, the paper propose a network structor seeing all 9 patch at the same time. Which is called CFN(context free network) siamese-ennead CNN.
8. In CFN the input patches goes in to same network(AlexNet) concurrently and concat before fc layer.
9. Fc layer learn the mapping of nine patches and their permutation.
10. Permutation used for training is setted(n. 60~100) and made for maximizing average hamming distance.
11. During the training pretext task, the network could fit wrong way. That's called shortcut. Learning shortcut means a network is fitted good for solving pretext tasks but bad at making general representation.
12. To avoid shortcut. The paper propose some techniques. Choosing good permutation, gapping the pieces, color maniplation(jittering and mixing with gray image) are those.

### Terms

- pretext task : task used for learning representation in transfer learning. In transfer learning process the representation is used for other tasks like detecton or classification.
- expoit : to utilize. (I knew that word is for abusing)
- chromatic aberration : Wrong focus makes each color channel shifts a little. light raies that have different frequency has different refractive index. If a ray pass through the lens, lens became a prism. To prevent that, typical camera has lots of lens and to move them to adjust the refract. (In korean 색수차)

### Introduction

Using supervised learning in visual task has been done successfully. But It's labeling work is labor-oriented. That makes unsupervised learning popular. Recetly proposed method called ***self-supervised learning*** uses label easily getted from image or out of that to learn general-purpose features. The paper review three different approach. One use relative position of two patches as label. Second one use video to learn object correspondence. Last one is on [here](https://arxiv.org/abs/1505.01596). The first one uses only sigle image (at a time). But other ones use multiple images. 
The paper suggest ***Jigsaw Puzzle*** as a pretext of self-supervised learning. To solve puzzle a model need to look all piece of it. Feature learned from this paper switches well to other tasks like detection or segmentation.

![puzzle example](https://github.com/Outerskyb/Outerskyb.github.io/blob/master/_posts/img/2021-11-30-Unsupervised-Learning-of-Visual-Representations-by-solving-Jigsaw-Puzzles/img1.JPG?raw=true)

### Related Work

later...

![fig2](https://github.com/Outerskyb/Outerskyb.github.io/blob/master/_posts/img/2021-11-30-Unsupervised-Learning-of-Visual-Representations-by-solving-Jigsaw-Puzzles/img2.JPG?raw=true)

### Solving Jigsaw Puzzles

Putting all piece of puzzle as a single input of models is not a good idea. That makes the network prefer to identify correlations between low-level texture rather than high-level primitives. Just looking at the boundaries of patches doesn't help for understanding the global object(like tiger in fig1). The target of model is learn features which are representive and discriminative while solving puzzle.

![fig3](https://github.com/Outerskyb/Outerskyb.github.io/blob/master/_posts/img/2021-11-30-Unsupervised-Learning-of-Visual-Representations-by-solving-Jigsaw-Puzzles/img4.JPG?raw=true)

### 3.1 The Context-Free Architecture

Dealing with these problem, the paper build siamese-ennead convolution neural network. Which is called Context free Network. From the input of it to fc6's structor is same as Alexnet's. The network uses this structor as row of siamese-ennead network. After data pass fc6 layer all nine ouput of fc6 layer is concatenated, Then feeded to fc7. All of the weights in siamese part are shared.

### 3.2 The jigsaw Puzzle Task

As difficult of using all 9! pemutation for training is hard, Paper define a set of permutation used for training. number of elements in set is 69 to 1000. permutation set is import factor on learning pretext and tranfer task.

### 3.3 Training the CFN

We can assume the ouput of CFN as the conditional pdf of the spatial arrangement of object parts in a part based model.

![fig4](https://github.com/Outerskyb/Outerskyb.github.io/blob/master/_posts/img/2021-11-30-Unsupervised-Learning-of-Visual-Representations-by-solving-Jigsaw-Puzzles/img5.JPG?raw=true)

The equation is true because
``
p(s|A) = p(s|F) * p(F|A) 
``
(if it doesn't come to you guess s = human male, F= human, A = animal)
