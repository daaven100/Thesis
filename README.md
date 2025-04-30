# Securing On-Device AI From Model Probing Attacks Using Autoencoder
## 1. Overview

This project shows how autoencoders can be used to detect black-box probing attacks on On-Device Machine Learning (ODML) systems. We developed a lightweight, anomaly-based defense mechanism that learns patterns of benign query activity and flags sequences that deviate from this behavior.

This repository includes implementations for both ImageNet and CIFAR-10 classification models, including adversarial testing scenarios. It also features a Variational Autoencoder (VAE) designed to generate synthetic benign samples to support training for ImageNet.

Each script has its required dependencies listed at the top of the file. Make sure to install them in your environment before running.

You can download the datasets here:  

Make sure to update the dataset paths in the scripts as needed.

## 2. ImageNet & CIFAR-10 Autoencoders

Both ImageNet and CIFAR-10 pipelines use the same medium-term convolutional autoencoder (AE) architecture, designed to detect anomalies in sequences of model queries. The AE monitors 600-query sequences and is trained to reconstruct benign behavior. High reconstruction error or stability deviations signal a potential attack.

Each AE script performs the following:
- Preprocessing 
- Training of the autoencoder model
- Evaluation against multiple black-box attacks 
- An adversarial injection test that simulates hidden attacks within longer benign query streams

Scripts included:
- `ImageNet_AE.py` – Full AE pipeline for ImageNet
- `CIFAR10_AE.py` – Full AE pipeline for CIFAR-10

## 3. ImageNet VAE for Synthetic Data

We implemented a Variational Autoencoder (VAE) for the ImageNet pipeline due to its limited benign data. This VAE is trained solely on real benign queries and generates synthetic samples that preserve the characteristics of actual queries.

The generated synthetic data was used to train the AE while using the original real dataset for testing only. This improves generalization and can reduce overfitting.

Script included:
- `ImageNet_VAE.py` – Trains a VAE and generates synthetic benign query samples
