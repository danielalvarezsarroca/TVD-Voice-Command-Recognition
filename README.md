# TVD-Voice-Command-Recognition with Deep Learning

This project explores different deep learning architectures for **voice command recognition** using **Mel-spectrograms** as input representations. The work has been developed as part of the course *Tractament de la Veu i el Diàleg* (UPC – FIB, Degree in Artificial Intelligence).

We systematically compare **convolutional, recurrent, hybrid and attention-based models**, as well as several **data augmentation techniques**, to analyze their impact on performance and generalization.

---

## Project Overview

The main objective of this project is to evaluate how different neural network architectures model audio signals for the task of **spoken command classification**, and to determine which approaches achieve the best performance.

The workflow of the project is:
1. Audio preprocessing and spectrogram generation
2. Comparison of different spectrogram types
3. Evaluation of multiple neural architectures
4. Application of data augmentation techniques
5. Global comparison and analysis of results

---

## Audio Representation

We initially compared different spectrogram representations using a **baseline CNN model**:

- Basic spectrogram
- Mel-spectrogram
- MFCC

### Conclusion
**Mel-spectrograms** consistently provided the best validation accuracy and were therefore used in all subsequent experiments.

---

## Models Evaluated

### Baseline Models
- **CNN (basic)**
- **CNN + Dropout**
- **RNN BiLSTM**
- **RNN BiGRU**

These models served as reference points to understand the impact of convolutional vs. recurrent modeling.

---

### Advanced Architectures

#### CNN
A deep convolutional network with multiple convolutional blocks and global average pooling, focused on extracting hierarchical time–frequency patterns.

#### CNN + BiGRU
A hybrid architecture combining:
- CNN layers for local feature extraction
- Bidirectional GRU for temporal modeling

This model already showed a significant improvement over pure CNN and RNN approaches.

#### CNN + BiGRU with Integrated Data Augmentation
The same hybrid architecture, but with **data augmentation layers integrated directly into the model**, applied only during training.  
This approach increased robustness and reduced overfitting.

#### Conformer (CNN + Self-Attention)
An attention-based architecture inspired by Conformer models:
- CNN front-end
- Positional encoding
- Multi-head self-attention blocks

This model captures long-range temporal dependencies more effectively than CNN–RNN architectures.

---

## Data Augmentation Techniques

To improve generalization, several augmentation strategies were tested:

### SpecAugment
- Time masking
- Frequency masking  
Applied only to the training set.

### Random Erasing
- Random removal of rectangular time–frequency regions
- Strong regularization effect

### SpecAugment + Random Erasing
Combination of both techniques to maximize variability in the training data.

---

## Results Summary

The following table summarizes the **best validation results** obtained for each relevant configuration:

```latex
\begin{table}[H]
\centering
\caption{Resumen global de resultados (Mel-spectrograms)}
\label{tab:global_results}
\begin{tabular}{lccc}
\toprule
\textbf{Modelo} & \textbf{Train Acc.} & \textbf{Val. Acc.} & \textbf{Val. Loss} \\
\midrule
CNN básico & 0.80 & 0.72 & 1.07 \\
CNN + Dropout & 0.74 & 0.77 & 0.87 \\
RNN BiLSTM & 0.93 & 0.91 & 0.31 \\
RNN BiGRU & 0.95 & 0.92 & 0.28 \\
CNN profundo & 0.97 & 0.93 & 0.24 \\
CNN + BiGRU & 0.98 & 0.95 & 0.20 \\
CNN + BiGRU + SpecAugment & 0.91 & 0.96 & 0.15 \\
CNN + BiGRU + Random Erasing & 0.86 & 0.96 & 0.15 \\
CNN + BiGRU + Aug. integrado & 0.96 & 0.95 & 0.18 \\
Conformer & 0.97 & 0.93 & 0.28 \\
\bottomrule
\end{tabular}
\end{table}

