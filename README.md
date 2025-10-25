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

    Alpha = 0.2 | Sigma = 0.5 | Architecture = 4000/2000/1000

    Tested under various poisoning-ratio and a fixed fine-tuning size of 5% (default), the following data shows that PBP achieves superior performance in purifying backdoor attacks whilst maintaining overall classifier accuracy.
  
    <table>
      <tr>
        <th rowspan="2">Poisoning<br>ratio (%)</th>
        <th colspan="2">Pre-trained</th>
        <th colspan="2">FT</th>
        <th colspan="2">FT-init</th>
        <th colspan="2">FE-tuning</th>
        <th colspan="2">LP</th>
        <th colspan="2">FST</th>
        <th colspan="2">PBP</th>
      </tr>
      <tr>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
        <th>C-Acc</th>
        <th>ASR</th>
      </tr>
      <tr>
        <td>0.5</td>
        <td>98.891</td>
        <td>96.057</td>
        <td>98.9265</td>
        <td>93.8695</td>
        <td>98.9795</td>
        <td>95.0848</td>
        <td>98.8865</td>
        <td>94.8518</td>
        <td>98.947</td>
        <td>92.5157</td>
        <td>98.7685</td>
        <td>94.8236</td>
        <td>95.8525</td>
        <td><strong>26.2152</strong></td>
      </tr>
      <tr>
        <td>1</td>
        <td>98.9325</td>
        <td>96.953</td>
        <td>98.888</td>
        <td>95.7123</td>
        <td>98.97</td>
        <td>95.4782</td>
        <td>98.957</td>
        <td>96.5579</td>
        <td>98.9615</td>
        <td>94.0193</td>
        <td>98.8</td>
        <td>96.1167</td>
        <td>96.001</td>
        <td><strong>27.9202</strong></td>
      </tr>
      <tr>
        <td>2</td>
        <td>98.882</td>
        <td>98.357</td>
        <td>98.9335</td>
        <td>96.5767</td>
        <td>98.975</td>
        <td>96.7089</td>
        <td>98.901</td>
        <td>97.1837</td>
        <td>98.9285</td>
        <td>96.5847</td>
        <td>98.867</td>
        <td>97.3399</td>
        <td>96.026</td>
        <td><strong>30.1084</strong></td>
      </tr>
      <tr>
        <td>5</td>
        <td>98.89</td>
        <td>99.21</td>
        <td>98.931</td>
        <td>98.931</td>
        <td>98.931</td>
        <td>98.6371</td>
        <td>98.871</td>
        <td>98.7244</td>
        <td>98.9475</td>
        <td>98.3852</td>
        <td>98.8565</td>
        <td>98.4523</td>
        <td>95.9555</td>
        <td><strong>32.5981</strong></td>
      </tr>
    </table>

  
2. **Is PBP effective against backdoor attacks carried out by attackers with varying levels of strength?**

    Alpha = 0.2 | Sigma = 0.5 | Architecture = 4000/2000/1000
    
    Evaluated across differing poisoning-ratio, PBP shows to be the only fine-tuning strategy that can mitigate the backdoor effect across various attacker-power settings.

    <img width="600" height="371" alt="chart (1)" src="https://github.com/user-attachments/assets/20b5e5d5-faec-4560-a7d3-834eebda09c7" />

3. **Can PBP purify backdoor attacks stably under different fine-tuning assumptions?**

    Alpha = 0.2 | Sigma = 0.5 | Architecture = 4000/2000/1000

    Evaluated under different fine-tuning size, from 1% to 10%, each with poisoning-ratios that ranges from 0.5% to 5%.
    
    PBP is confirmed to be the most effective and stable approach across different fine-tuning sizes.

    <img width="458" height="283" alt="Fine-tuning Size = 1%" src="https://github.com/user-attachments/assets/4dfe6261-a61c-475b-ae5b-1d690d39fd94" />

    <img width="458" height="283" alt="Fine-tuning Size = 2%" src="https://github.com/user-attachments/assets/a47d5e35-590b-486e-aba0-b4d018eccb4f" />

    <img width="458" height="283" alt="Fine-tuning Size = 5%" src="https://github.com/user-attachments/assets/2df70661-9608-4df2-acde-dbcc2efb0e06" />

    <img width="458" height="283" alt="Fine-tuning Size = 10%" src="https://github.com/user-attachments/assets/e9aca412-9050-4977-8149-760e1b1d9eff" />


5. **How is PBP’s efficiency and sensitivity to its hyperparameters and model architectures?**

    Experimented under differing alpha, sigma, and architecture (number of BN layers).

    \<TO BE CONTINUED>

---

## Acknowledgments
- **Computing Resources**: Chameleon Cloud (CHI@UC) for providing GPU infrastructure
- **Original Authors**: For making the training code publicly available
- **NDSS 2025**: For publishing the foundational research
---
