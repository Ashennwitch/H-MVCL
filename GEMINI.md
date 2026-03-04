# Res-HMVCL: Residual Heterogeneous Multi-View Contrastive Learning

## Project Overview
**Res-HMVCL** is a deep learning framework designed for encrypted network traffic classification (e.g., SSL/TLS) under conditions of extreme label scarcity. It addresses the limitations of Deep Packet Inspection (DPI) by using flow-based analysis.

The core innovation is a **Multi-View** approach that combines:
1.  **1D-CNN Payload Representations:** Analyzing raw packet bytes.
2.  **Bi-directional Flow Statistics:** Analyzing statistical features (and potentially Spectral/FFT features).

These views are integrated via a **residual contrastive mechanism**. The model employs **Universal Contrastive Pre-training** to learn from unlabeled data, achieving high performance (94% F1-Score on ISCXVPN2016) with only 20% labeled data.

## Project Structure & Workflow
The project is organized into a sequence of Jupyter Notebooks representing the experimental pipeline:

### Core Pipeline
1.  **`01_build_pretrain_data.ipynb`**: Data preparation. Generates the two "views" (Raw Payload and Stats) from the source network traffic data.
2.  **`02_train_hmvcl.ipynb`**: Pre-training phase. Trains the encoders using Contrastive Learning (NT-Xent loss) on unlabeled data to learn traffic manifolds.
3.  **`03_finetune_multitask.ipynb`**: Fine-tuning phase. Uses the pre-trained encoders and a small amount of labeled data to train the final classifiers (Binary and Category).

### Baselines & Experiments
*   `04_baseline_stats_only.ipynb`: Baseline using only statistical features.
*   `05_baseline_supervised_cnn.ipynb`: Baseline using a standard supervised CNN.
*   `06_baseline_deeppacket.ipynb`: Implementation of the "Deep Packet" approach.
*   `07_baseline_simclr_pretrain.ipynb`: Baseline using SimCLR (a standard contrastive learning method).
*   `08_baseline_deep_fusion.ipynb`: Baseline using Deep Fusion.
*   `09_feature_ablation.ipynb`: Feature ablation studies.

### Documentation & Paper
*   `main.tex`: The LaTeX source code for the research paper describing this work.
*   `references.bib`: Bibliography for the paper.
*   `README.md`: Project summary.

## Key Technologies
*   **Language:** Python
*   **Frameworks:** TensorFlow, Keras
*   **Libraries:** NumPy, Pandas, Scikit-learn
*   **Documentation:** LaTeX (IEEEtran class)

## Usage
To replicate the experiments:
1.  **Data Setup:** Ensure the ISCXVPN2016 dataset (or equivalent) is available. Update paths in `01_build_pretrain_data.ipynb` (e.g., `BASE_PATH`).
2.  **Execution Order:** Run the notebooks in numerical order (01 -> 02 -> 03).
3.  **Configuration:** Key hyperparameters (Batch Size, Epochs, Learning Rate, Temperature) are defined at the top of the notebooks.

## Development Conventions
*   **Code Style:** Research code in Jupyter Notebooks.
*   **Data Handling:** Large datasets are processed into `.npy` files for efficient loading during training.
*   **Model Architecture:** Custom Keras `Model` classes are used for the Encoders and the HMVCL wrapper.
