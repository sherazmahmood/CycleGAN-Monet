# CycleGAN: Monet Style Transfer
By Sheraz Mahmood

Kaggle Competition: https://kaggle.com/competitions/gan-getting-started

## **Objective**

The goal of this project is to build a deep learning model capable of converting real-world photographs into Monet-style paintings. We aim to replicate not just the color palette, but also the textural brushstroke patterns and vibrant impressionistic style characteristic of Claude Monet's artwork. The final output should not only be visually convincing but stylistically faithful to Monet's work.

## **Approach**

We implement a few slightly modified CycleGAN architectures. 
- Two Generators: Photo to Monet then Monet to Photo
- Two Discriminators: one to discriminate Monet pictures and one to discriminate real photos
- Cycle Consistency: to preserve content during translation
- Identity and Adversarial loss

To improve the generators output we attempted:
- Perceptual loss using VGG19 this is to encourage high-level visual features alignment
- Colorfulness loss to mtain Monet's vibrat and saturated color style
- UpSampling vs. Conv2DTranspose to reduce checkerboard appearance.


Major challange is the brush strokes, the texture expressive, layered brush strokes. 

Results: 
![Alt Text](output-run2.gif)
![Alt Text](output-run3.gif)
![Alt Text](output-run4.gif)
![Alt Text](output-run5.gif)
