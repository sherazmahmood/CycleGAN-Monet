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

This repository contains a full implementation of a CycleGAN model trained to transform real photographs into paintings in the style of Claude Monet, built for the [Kaggle "GANs Getting Started" competition](https://www.kaggle.com/competitions/gan-getting-started). The model is trained using TensorFlow/Keras and is optimized to produce high-quality, stylistically consistent Monet-style images.

## Project Goal

To develop a deep learning model that can learn the mapping between real-world photographs and Monet-style paintings without requiring paired image datasets. The model should be able to generate artistic outputs that retain scene structure while reflecting stylistic brush strokes and color patterns characteristic of Monet.

## Model Architecture

The solution is based on the [CycleGAN](https://arxiv.org/abs/1703.10593) framework. Key components include:

- **Two Generators (G and F)**:
  - G: Photo → Monet
  - F: Monet → Photo

- **Two Discriminators (D_X and D_Y)**:
  - D_X: Distinguishes real vs. fake photos
  - D_Y: Distinguishes real vs. fake Monet images

- **Losses**:
  - Adversarial Loss (LSGAN)
  - Cycle Consistency Loss
  - Identity Loss
  - Perceptual Loss (using VGG19)
  - Colorfulness Loss (optional, tuned during experimentation)

- **Enhancements Tried**:
  - Skip connections between input and output
  - Replacement of `Conv2DTranspose` with `UpSampling + Conv2D` to reduce checkerboard artifacts
  - Learning rate scheduling and progressive tuning
  - Experiments with style loss using Gram matrices

## Evaluation Metric

This project is evaluated on the **MiFID (Memorization-informed Fréchet Inception Distance)** score, which penalizes both low realism and overfitting/memorization of training images. MiFID is computed using:
- FID distance between distributions of generated and real images
- A memorization term that penalizes over-similarity to training examples

## Dataset

- **Source**: Provided by the Kaggle competition
- **Structure**:
  - `monet_jpg/` – 300 Monet paintings
  - `photo_jpg/` – 7038 real-world photographs
  - `test_jpg/` – Test photos to generate Monet-style outputs

- **Image Size**: All images are resized to `256x256x3` and normalized to `[-1, 1]`.

## Training Details

- **Hardware**: Trained on Google Colab with NVIDIA A100

- Results:

![Alt Text](output-run2.gif)
![Alt Text](output-run3.gif)
![Alt Text](output-run4.gif)
![Alt Text](output-run5.gif)
