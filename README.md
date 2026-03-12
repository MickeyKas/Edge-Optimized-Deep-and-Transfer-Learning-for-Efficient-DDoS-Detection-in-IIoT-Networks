# Edge-Optimized-Deep-and-Transfer-Learning-for-Efficient-DDoS-Detection-in-IIoT-Networks
Lightweight CNN-CBAM DDoS Detector for IIoT Edge Gateways

A lightweight deep learning framework for real-time DDoS detection on Industrial IoT (IIoT) edge gateways using a hybrid CNN + CBAM attention + MLP classifier architecture with transfer learning between CIC-DDoS2019 and CICIoT23 datasets.

The system is designed for sub-millisecond inference latency, making it suitable for resource-constrained edge devices.

Overview

Industrial IoT infrastructures are increasingly exposed to distributed denial-of-service (DDoS) attacks, which can disrupt critical systems such as manufacturing, energy grids, and smart infrastructure.

Traditional detection methods often struggle with:

High-volume traffic

Real-time processing constraints

Resource limitations on edge gateways

This project proposes a lightweight deep neural network architecture capable of detecting DDoS attacks with high accuracy while maintaining real-time performance.

Key features:

CNN feature extractor for temporal traffic patterns

CBAM attention module to highlight important features

MLP classifier for final decision

Projection layer enabling transfer learning across datasets with different feature sizes

Designed for CPU-only edge deployment

Architecture

The proposed UnifiedDetector pipeline:

Input Features
      │
      ▼
Feature Projection (F → 39)
      │
      ▼
Reshape (B,1,39)
      │
      ▼
CNN Feature Extractor
(3 Convolution Layers + CBAM Attention)
      │
      ▼
Global Average Pooling
      │
      ▼
Feature Concatenation
(skip connection from projection)
      │
      ▼
MLP Classifier
      │
      ▼
Sigmoid Output
(Attack / Normal)

The architecture balances accuracy and computational efficiency for edge environments.

Datasets

Two publicly available cybersecurity datasets were used.

CIC-DDoS2019

Large-scale dataset containing various DDoS attack scenarios.

Features:

Network traffic statistics

Flow-based features

Multiple attack types

CICIoT2023

A modern dataset representing IoT network traffic and attacks.

Characteristics:

Realistic IoT device traffic

Highly imbalanced dataset

Suitable for transfer learning experiments

Experimental Setup

Experiments were conducted in two stages.

1. Pre-training

The model is first trained on:

CIC-DDoS2019

to learn general network traffic patterns.

Best validation accuracy achieved:

97.31%
2. Transfer Learning / Fine-tuning

The pretrained model is then fine-tuned on CICIoT23.

This allows the detector to adapt to IoT-specific traffic behaviour.

Best validation accuracy:

99.50%

Training converges within 8 epochs.

Test Performance
Metric	CIC-DDoS2019	CICIoT23
Accuracy	97.26%	99.52%
Precision	0.9707	0.9986
Recall	0.9946	0.9965
F1 Score	0.9825	0.9975
AUC	0.9817	0.9990

The detector achieves near-perfect recall, ensuring almost no attacks are missed.

Real-Time Performance

The model is designed for edge gateway deployment.

Metric	Value
Average latency	0.011 ms
P99 latency	0.017–0.019 ms
Throughput	≈ 88k–93k packets/s
Batch throughput	≈ 37,800 packets/s
Operations per inference	~274,944 FLOPs
Resource Usage

Batch evaluation on the CICIoT23 test set (1,176,851 samples):

Execution time : 31.07 s
Memory usage   : ~265 MB

Memory usage is mainly due to the Python runtime and dataset loader, not the model itself.

Real-Time Schedulability

Using fixed-priority scheduling:

Execution time (C) = 0.011 ms
Period (T) = 1 ms
Utilisation U = 0.61

Liu-Layland bound for two tasks:

U_bound = 0.828

Since:

U < U_bound

the detector is schedulable in real-time systems.

Repository Structure
project/
│
├── notebooks/
│   ├── training_pipeline.ipynb
│   └── evaluation.ipynb

│
├── results/
│   └── experiment_outputs
│
└── README.md
Requirements

Python 3.10+

Key libraries:

torch
numpy
pandas
scikit-learn
matplotlib
seaborn
psutil

Install dependencies:

pip install -r requirements.txt
Running the Experiments
1. Pre-training
python train_ddos2019.py
2. Fine-tuning
python finetune_ciciot23.py
3. Evaluation
python evaluate_model.py
Applications

The proposed system can be deployed in:

Industrial IoT gateways

Smart manufacturing networks

Edge security appliances

Software-defined networking controllers

Real-time intrusion detection systems

Future Work

Future improvements may include:

Multi-class attack classification

Adaptive detection thresholds

Online learning for evolving attacks

Deployment on ARM-based industrial hardware

Integration with SDN mitigation frameworks

License

This project is released under the MIT License.

Citation
Mikiyas et al
Edge-Optimized-Deep-and-Transfer-Learning-for-Efficient-DDoS-Detection-in-IIoT-Networks
