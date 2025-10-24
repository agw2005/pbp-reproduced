# Reproduced The Novel Fine-tuning Defense Solution From The 2025 NDSS Publication

> **Dung Thuy Nguyen, Ngoc N. Tran, Taylor T. Johnson, Kevin Leach**  
> *Network and Distributed System Security Symposium (NDSS), 2025*  
> [[Paper](https://arxiv.org/pdf/2412.03441)] | [[Video]()] | [[Original source code](https://github.com/judydnguyen/pbp-backdoor-purification-official)]

---

## Overview

This repository contains a reproduction attempt for the experiments from the NDSS 2025 publication. The project focuses on purifying a malware classifier model that has been breached by a backdoor poisoning attack at differing poisoning-ratios by utilizing a small subset of clean fine-tuning data in order to maintain high accuracy on overall classifier capability whilst reducing the success-rate of the attack.

---

### Model Training
- **GPU Infrastructure**: Chameleon Cloud GPU (NVIDIA Quadro RTX 6000) at CHI@UC
- **Processor Infrastructure**: Chameleon Cloud CPU (Intel(R) Xeon(R) Gold 6126 CPU @ 2.60GHz) at CHI@UC
- **Platform**: https://chameleoncloud.org/
- **Dataset**: Ember
- **Hyperparameter**: 
  - Poisoning-ratio (0.5%, 1%, 2%, 5%)
  - Fine-tuning size (10%, 5%, 2%, 1%)
- **Metric**: 
  - C-Acc (Classifier Accuracy)
  - ASR (Attack Success-Rate)

### Results
1. **How well does PBP purify backdoor attacks compared to related fine-tuning methods?**

  Tested under various poisoning-ratio and a fixed fine-tuning size of 5% (default), the following data shows that PBP achieves superior performance in purifying backdoor attacks.
  <img width="1820" height="313" alt="image" src="https://github.com/user-attachments/assets/d9f30d70-0331-456f-a527-ec5bede26c99" />
3. Is PBP effective against backdoor attacks carried out by attackers with varying levels of strength?
4. Can PBP purify backdoor attacks stably under different fine-tuning assumptions?
5. How is PBP’s efficiency and sensitivity to its hyperparameters and model architectures?

---

## Acknowledgments
- **Computing Resources**: Chameleon Cloud (CHI@UC) for providing GPU infrastructure
- **Original Authors**: For making the training code publicly available
- **NDSS 2025**: For publishing the foundational research
---
