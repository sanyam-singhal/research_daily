+++
title = "Deep Domain Isolation and Sample Clustered Federated Learning for Semantic Segmentation"
date = 2024-10-22
description = "Introduces Deep Domain Isolation and Sample Clustered Federated Learning for improved performance in Non-IID settings."

[extra]
paper_tags = "Federated Learning, Semantic Segmentation, Domain Isolation, Covariate Shift"
cover_path = "/deep-domain-isolation-scfl-for-segmentation.png"
cover_alt="Overview of the Sample Clustered Federated Learning (SCFL) framework.It is composed of four sequential blocks."
display_date = "October 22, 2024"
reference_link = "https://arxiv.org/pdf/2410.14693"
+++

# Sample Clustered Federated Learning for Semantic Segmentation {.contentTitleStyle}

## Introduction: Tackling Covariate Shifts in Federated Learning {.contentSectionHeader}

Federated learning (FL) has emerged as a powerful tool for training models on decentralized datasets without compromising data privacy. However, FL faces challenges when dealing with Non-Independent and Identically Distributed (Non-IID) data across participating clients. While previous research focused on label or concept shifts, this paper dives into the impact of *covariate shifts*—variations in data distributions—on the performance of federated learning for 2D semantic segmentation.

We find that covariate shifts, although less impactful than label shifts, still hinder convergence in FL for semantic segmentation.  To address this, we propose a novel framework called **Sample Clustered Federated Learning (SCFL)**. This innovative approach significantly improves convergence speed and generalization performance compared to existing techniques.

## Understanding Covariate Shifts and Existing Limitations {.contentSectionHeader}

Covariate shifts represent differences in the underlying feature distributions of data across clients. Unlike label shifts (differences in class distributions) or concept shifts (differences in task definitions), covariate shifts affect the model's ability to generalize to unseen data.  Existing personalized and clustered federated learning methods often fall short in scenarios where each client's data encompasses multiple underlying feature domains. These methods typically operate at the *client level*, assuming homogeneity within each client's dataset. This assumption is frequently violated in real-world applications.

## The Sample Clustered Federated Learning (SCFL) Framework {.contentSectionHeader}

SCFL introduces a sample-level clustering approach to overcome these limitations.  It leverages a novel technique called **Deep Domain Isolation (DDI)** to identify and isolate image domains directly in the model's gradient space. This is achieved using a Federated Gaussian Mixture Model (Fed-GMM) and spectral clustering.  The key steps of SCFL are:

1.  **Federated Pretraining:**  Initializes a global model using FedAvg.
2.  **Clustering using DDI:** Isolates image domains at the sample level using gradient analysis. A pruned version of DDI is also introduced to mitigate computational costs.
3.  **Sample Clustered Federated Refinement:** Trains independent models for each isolated domain using FedAvg.
4.  **Test-Time Cluster Assignment:** Assigns test samples to their corresponding domains using a trained classifier, eliminating the need for assumptions about the test data distribution.

## Experimental Results and Validation {.contentSectionHeader}

Experiments were conducted on both synthetic (TMNIST-Inv) and real-world (Cityscapes+GTA5) datasets with various data splits (IID, Full non-IID, Dirichlet non-IID) to simulate different levels of data heterogeneity.  The results demonstrate:

*   Covariate shifts negatively impact the convergence of standard FedAvg, especially in Full non-IID settings.
*   SCFL significantly outperforms all baseline methods (FedAvg, SCAFFOLD, personalized FedAvg+, and CFL) across all data splits and datasets, particularly in Non-IID scenarios.  This improvement is measured by a substantial increase in mean Intersection over Union (mIoU).
*   DDI effectively isolates image domains, exhibiting high clustering accuracy.
*   The test-time cluster assignment mechanism accurately assigns test samples to the correct domains.
*   Pruned DDI maintains high performance even with significant gradient pruning.

## Conclusion and Future Directions {.contentSectionHeader}

SCFL presents a robust framework for handling covariate shifts in federated learning for semantic segmentation. Its sample-level approach improves convergence, generalization, and offers a solution that is agnostic to test distribution assumptions.

Future research could explore alternative clustering techniques, investigate the impact of different model architectures, extend SCFL to handle multiple types of Non-IID data, and apply it to other computer vision tasks.  Further investigation into computational efficiency and scalability is also warranted.




