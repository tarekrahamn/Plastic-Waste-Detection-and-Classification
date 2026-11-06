<div align="center">

# Plastic Waste Detection and Classification

### An AI-powered object-detection study to identify and classify plastic waste using YOLO-based deep learning models.

<p>
  <a href="https://github.com/tarekrahamn/Plastic-Waste-Detection-and-Classification">
    <img src="https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github" alt="GitHub repository">
  </a>
  <img src="https://img.shields.io/badge/Task-Object%20Detection-2563EB?style=for-the-badge" alt="Object detection">
  <img src="https://img.shields.io/badge/Framework-Ultralytics-7C3AED?style=for-the-badge" alt="Ultralytics">
  <img src="https://img.shields.io/badge/Models-YOLOv8%20%7C%20YOLO12%20%7C%20YOLO26-059669?style=for-the-badge" alt="YOLO models">
  <a href="https://doi.org/10.17632/wsxmhf8sgv.2">
    <img src="https://img.shields.io/badge/Dataset-DOI%3A%2010.17632%2Fwsxmhf8sgv.2-0A7B83?style=for-the-badge" alt="Dataset DOI">
  </a>
</p>

**Repository:** [tarekrahamn/Plastic-Waste-Detection-and-Classification](https://github.com/tarekrahamn/Plastic-Waste-Detection-and-Classification)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Objectives](#objectives)
- [Detection Categories](#detection-categories)
- [Dataset](#dataset)
- [Dataset Statistics](#dataset-statistics)
- [Methodology](#methodology)
- [Experimental Setup](#experimental-setup)
- [Model Performance](#model-performance)
- [Visual Results](#visual-results)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Reproducibility Notes](#reproducibility-notes)
- [Limitations and Future Work](#limitations-and-future-work)
- [Authors and Contributions](#authors-and-contributions)
- [Citation](#citation)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Overview

Plastic pollution is a significant environmental challenge. Efficient identification of plastic waste in images can support waste monitoring, sorting, and environmental assessment workflows.

This project investigates deep-learning-based **plastic waste object detection and category recognition** using three YOLO model variants: **YOLOv8s, YOLO12s, and YOLO26s**. The models are fine-tuned on a five-category plastic-waste dataset and evaluated using standard object-detection metrics.

The repository provides the training notebooks and selected evaluation visualizations for the three model experiments.

> **Task clarification:** The implemented pipeline is object detection. It predicts bounding boxes and assigns a waste-category label to each detected object. It is not a separate image-level classification pipeline.

## Objectives

- Develop an object-detection workflow for identifying common plastic-waste items.
- Train and evaluate YOLOv8s, YOLO12s, and YOLO26s under a consistent high-level training setup.
- Compare model performance using Precision, Recall, F1-score, mAP@50, and mAP@50–95.
- Examine model behaviour through precision–recall curves, F1 curves, and confusion matrices.
- Provide a reproducible starting point for further research on automated plastic-waste monitoring.

## Detection Categories

The dataset contains five object categories:

| Class ID | Category |
|---:|---|
| 1 | Plastic-Bottle |
| 2 | Plastic-Cup |
| 3 | Plastic-Packet |
| 4 | Plastic-Straw |
| 5 | Polythene |

The IDs above are presented as an illustrative ordered list. Confirm the exact class-ID mapping against the dataset's `data.yaml` before using numeric IDs in downstream code.

## Dataset

The experiments use the **Plastic Waste Detection Dataset**, with the dataset record identified by the following DOI:

- **DOI:** [10.17632/wsxmhf8sgv.2](https://doi.org/10.17632/wsxmhf8sgv.2)
- **Dataset record:** [Mendeley Data](https://data.mendeley.com/datasets/wsxmhf8sgv/2)
- **License stated for the dataset:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Dataset workflow/source platform:** [Roboflow](https://roboflow.com/)

The dataset's DOI record is the source of record for dataset attribution and reuse conditions. Please review the original dataset record before redistributing dataset files.

### Dataset split

The dataset contains **6,356 images** and **7,918 annotations** across the training, validation, and test subsets.

## Dataset Statistics

| Split | Images | Image Share | Annotations | Annotation Share | Avg. Annotations / Image | Multi-object Images |
|---|---:|---:|---:|---:|---:|---:|
| Training | 4,449 | 70.0% | 5,551 | 70.1% | 1.25 | 726 (16.3%) |
| Validation | 1,271 | 20.0% | 1,578 | 19.9% | 1.24 | 205 (16.1%) |
| Test | 636 | 10.0% | 789 | 10.0% | 1.25 | 92 (14.5%) |
| **Total** | **6,356** | **100%** | **7,918** | **100%** | **1.25** | **1,023 (16.1%)** |

*Dataset split statistics are transcribed from the project research table supplied by the authors.*

## Methodology

The experimental workflow consists of dataset preparation, model fine-tuning, validation, and comparative evaluation.

```mermaid
flowchart TD
    A[Plastic Waste Dataset] --> B[Dataset preparation and export]
    B --> C[Train / Validation / Test split]
    C --> D1[YOLOv8s]
    C --> D2[YOLO12s]
    C --> D3[YOLO26s]
    D1 --> E[Model training]
    D2 --> E
    D3 --> E
    E --> F[Validation and prediction]
    F --> G[Precision, Recall, F1, mAP]
    G --> H[Comparative analysis]
```

### Model training

Three small YOLO model variants were trained:

- **YOLOv8s**
- **YOLO12s**
- **YOLO26s**

The notebooks use pretrained model weights and fine-tune them for the five target classes.

### Evaluation metrics

- **Precision:** The proportion of predicted detections that are correct.
- **Recall:** The proportion of ground-truth objects that are successfully detected.
- **F1-score:** The harmonic mean of Precision and Recall.
- **mAP@50:** Mean Average Precision at an IoU threshold of 0.50.
- **mAP@50–95:** Mean Average Precision averaged over IoU thresholds from 0.50 to 0.95.

## Experimental Setup

| Parameter | Configuration |
|---|---|
| Framework | Ultralytics |
| Model variants | YOLOv8s, YOLO12s, YOLO26s |
| Training epochs | 50 |
| Input image size | 640 × 640 |
| GPU environment | NVIDIA Tesla T4 × 2 |
| Platform | Kaggle |
| Task | Object detection |
| Number of classes | 5 |
| Training status | All three models successfully trained |

The notebooks are designed to run in Kaggle and include installation, dataset access, training, validation, prediction, and result-archiving steps.

## Model Performance

The following values are the **final research-paper comparison results supplied by the authors**.

| Model | Epochs | mAP@50 | Precision | Recall | F1-score | mAP@50–95 |
|---|---:|---:|---:|---:|---:|---:|
| YOLOv8s | 50 | 0.903 | 0.910 | **0.850** | 0.882 | 0.671 |
| YOLO12s | 50 | **0.908** | 0.920 | 0.840 | **0.888** | 0.670 |
| YOLO26s | 50 | 0.907 | **0.923** | 0.845 | 0.882 | **0.681** |

### Key observations

- **YOLO12s** achieved the highest mAP@50 (0.908) and F1-score (0.888).
- **YOLO26s** achieved the highest Precision (0.923) and mAP@50–95 (0.681).
- **YOLOv8s** achieved the highest Recall (0.850).
- The results show a close performance comparison across the three model variants; the most suitable model depends on the metric and application priorities.

*The values above are reported as provided in the authors' final comparison table. They are not recomputed in this README.*

## Visual Results

The `Figures/` directory contains the saved model evaluation plots. The following figures are embedded directly from the repository.

### YOLOv8

| Confusion Matrix | Normalized Confusion Matrix |
|---|---|
| ![YOLOv8 confusion matrix](Figures/YOLOv8/confusion_matrix.png) | ![YOLOv8 normalized confusion matrix](Figures/YOLOv8/confusion_matrix_normalized.png) |

| Precision–Recall Curve | F1 Curve |
|---|---|
| ![YOLOv8 PR curve](Figures/YOLOv8/PR_curve.png) | ![YOLOv8 F1 curve](Figures/YOLOv8/F1_curve.png) |

| Precision Curve | Recall Curve |
|---|---|
| ![YOLOv8 precision curve](Figures/YOLOv8/P_curve.png) | ![YOLOv8 recall curve](Figures/YOLOv8/R_curve.png) |

### YOLO12

| Training Results | Confusion Matrix |
|---|---|
| ![YOLO12 training results](Figures/YOLOv12/results.png) | ![YOLO12 confusion matrix](Figures/YOLOv12/confusion_matrix.png) |

| Normalized Confusion Matrix | Precision–Recall Curve |
|---|---|
| ![YOLO12 normalized confusion matrix](Figures/YOLOv12/confusion_matrix_normalized.png) | ![YOLO12 PR curve](Figures/YOLOv12/BoxPR_curve.png) |

| F1 Curve | Precision and Recall Curves |
|---|---|
| ![YOLO12 F1 curve](Figures/YOLOv12/BoxF1_curve.png) | [Precision curve](Figures/YOLOv12/BoxP_curve.png) · [Recall curve](Figures/YOLOv12/BoxR_curve.png) |

### YOLO26

| Training Results | Confusion Matrix |
|---|---|
| ![YOLO26 training results](Figures/YOLOv26/results.png) | ![YOLO26 confusion matrix](Figures/YOLOv26/confusion_matrix.png) |

| Normalized Confusion Matrix | Precision–Recall Curve |
|---|---|
| ![YOLO26 normalized confusion matrix](Figures/YOLOv26/confusion_matrix_normalized.png) | ![YOLO26 PR curve](Figures/YOLOv26/BoxPR_curve.png) |

| F1 Curve | Precision and Recall Curves |
|---|---|
| ![YOLO26 F1 curve](Figures/YOLOv26/BoxF1_curve.png) | [Precision curve](Figures/YOLOv26/BoxP_curve.png) · [Recall curve](Figures/YOLOv26/BoxR_curve.png) |

## Repository Structure

```text
Plastic-Waste-Detection-and-Classification/
│
├── Code/
│   ├── YOLOv8.ipynb
│   ├── YOLOv12.ipynb
│   └── YOLOv26.ipynb
│
├── Figures/
│   ├── YOLOv8/
│   │   ├── confusion_matrix.png
│   │   ├── confusion_matrix_normalized.png
│   │   ├── F1_curve.png
│   │   ├── PR_curve.png
│   │   ├── P_curve.png
│   │   └── R_curve.png
│   │
│   ├── YOLOv12/
│   │   ├── results.png
│   │   ├── confusion_matrix.png
│   │   ├── confusion_matrix_normalized.png
│   │   ├── BoxF1_curve.png
│   │   ├── BoxPR_curve.png
│   │   ├── BoxP_curve.png
│   │   └── BoxR_curve.png
│   │
│   └── YOLOv26/
│       ├── results.png
│       ├── confusion_matrix.png
│       ├── confusion_matrix_normalized.png
│       ├── BoxF1_curve.png
│       ├── BoxPR_curve.png
│       ├── BoxP_curve.png
│       └── BoxR_curve.png
│
└── README.md
```

## Getting Started

### Requirements

- A Kaggle account (recommended, as the notebooks are configured for Kaggle).
- Internet access enabled in the notebook environment to install packages and retrieve the dataset.
- A GPU accelerator. The reported experiments used an NVIDIA T4 × 2 environment.
- Access to the dataset through its source/export workflow.

### Run the notebooks on Kaggle

1. Open the repository and navigate to the `Code/` directory.
2. Open the notebook for the model you want to run.
3. Import or upload the notebook into Kaggle.
4. In **Notebook Settings**, enable a GPU accelerator and turn Internet access on.
5. Install the dependencies using the installation cell in the notebook.
6. Configure your Roboflow credentials and dataset project/version details.
7. Run the notebook cells in order to download the dataset, train the model, validate it, and generate predictions.

### Notebooks

| Model | Notebook |
|---|---|
| YOLOv8s | [`Code/YOLOv8.ipynb`](Code/YOLOv8.ipynb) |
| YOLO12s | [`Code/YOLOv12.ipynb`](Code/YOLOv12.ipynb) |
| YOLO26s | [`Code/YOLOv26.ipynb`](Code/YOLOv26.ipynb) |

### Dependency installation

The notebooks install the required packages through pip. A typical installation command is:

```bash
pip install -U ultralytics supervision roboflow
```

**Version note:** The YOLOv8 notebook uses an Ultralytics version constraint, while the YOLO12 and YOLO26 notebooks use their own notebook-specific setup. For the closest reproduction of the reported experiments, follow the installation cells in each notebook rather than assuming one shared package version.

### Dataset credentials and configuration

The notebooks contain placeholder Roboflow credentials and project identifiers. Before running them:

- Add your own Roboflow API key and project/version details.
- Do not commit API keys, passwords, or private tokens to GitHub.
- Prefer Kaggle Secrets or environment variables for sensitive credentials.
- Ensure the downloaded dataset export is compatible with the notebook's YOLO data configuration (`data.yaml`).

### Training configuration

The notebooks use 50 epochs and an image size of 640 pixels. The YOLO training command follows this general pattern:

```bash
yolo task=detect mode=train \
  model=yolov8s.pt \
  data=/path/to/dataset/data.yaml \
  epochs=50 \
  imgsz=640 \
  plots=True
```

For YOLO12 and YOLO26, replace the model checkpoint with the corresponding model variant used in the relevant notebook.

## Reproducibility Notes

- Dataset versions and export formats should be kept consistent when comparing runs.
- Record the Ultralytics, PyTorch, CUDA, and Python versions used for each experiment.
- Keep the train/validation/test split fixed when reproducing the reported comparison.
- Use the same evaluation settings and confidence/IoU conventions across models.
- Store the best model weights and complete validation logs alongside the generated plots if you plan to publish or extend the experiments.
- The repository currently contains notebooks and selected figures; the dataset files and trained weight files are not included in the listed repository structure.

## Limitations and Future Work

### Current limitations

- The experiments cover five plastic-waste categories; performance on other waste types is not established by these results.
- The reported comparison focuses on object-detection metrics. Deployment latency, throughput, memory consumption, and edge-device performance are not reported in the supplied comparison table.
- The repository does not include the full dataset or trained model checkpoints, so reproducing the exact experiment requires access to the dataset and retraining or separately obtaining the weights.
- The reported results should be interpreted in the context of the dataset and evaluation protocol used in the study.

### Future work

- Extend the dataset with additional waste categories and more diverse environmental conditions.
- Evaluate robustness under varying lighting, occlusion, scale, and background complexity.
- Report inference speed (FPS), model size, parameter count, and computational cost.
- Explore real-time deployment for smart waste monitoring and automated sorting systems.
- Evaluate generalization on independent datasets and real-world images.

## Authors and Contributions

### Authors

| Author | GitHub |
|---|---|
| **Tarek Rahman** (T. R.) — Project Owner | [@tarekrahamn](https://github.com/tarekrahamn) |
| **Mst. Asifa Khatun** (M. A. K.) | [@islamasifa223-boop](https://github.com/islamasifa223-boop) |
| **Afsana Mimi** (A. M.) | [@afsanamimi5799](https://github.com/afsanamimi5799) |
| **Mst. Farha Musharrat Monira** (M. F. M. M.) | [@Farha-Musharrat-Monira](https://github.com/Farha-Musharrat-Monira) |

### CRediT Author Contributions

- **Tarek Rahman (T. R.):** Conceptualization, Methodology, Formal analysis, Dataset design, Supervision of the annotation process, Investigation, Training and evaluation of multiple object-detection models, Visualization, Writing – original draft, Writing – review and editing, and Supervision.
- **Mst. Asifa Khatun (M. A. K.):** Conceptualization, Formal analysis, Data curation, Validation, Methodology, and Data annotation.
- **Afsana Mimi (A. M.):** Conceptualization, Formal analysis, Data curation, Validation, Methodology, and Data annotation.
- **Mst. Farha Musharrat Monira (M. F. M. M.):** Conceptualization, Formal analysis, Data curation, Validation, Methodology, and Data annotation.

All authors have read and approved the final version of the manuscript.

## Citation

If you use the dataset, please cite its original record and follow the associated attribution requirements:

```text
Plastic Waste Detection Dataset.
Mendeley Data.
DOI: 10.17632/wsxmhf8sgv.2
```

Dataset DOI: https://doi.org/10.17632/wsxmhf8sgv.2

If this repository or its experimental results are used in academic work, please also cite the associated research paper when its full bibliographic details are available.

## License

No software license has been specified for this repository in this README. 

The dataset is identified as **CC BY 4.0**. This dataset license does not automatically apply to the source code in this repository. Review the dataset's original record and attribution requirements before redistributing dataset material.

## Acknowledgements

- [Ultralytics](https://www.ultralytics.com/) for the YOLO framework and documentation.
- [Roboflow](https://roboflow.com/) for dataset management and export workflow.
- [Mendeley Data](https://data.mendeley.com/) for dataset hosting and DOI-based access.
- Kaggle for the notebook execution environment used in the experiments.

---

<div align="center">

**Plastic Waste Detection and Classification**  
*Deep Learning for a Cleaner Environment*

[Repository](https://github.com/tarekrahamn/Plastic-Waste-Detection-and-Classification) · [Dataset DOI](https://doi.org/10.17632/wsxmhf8sgv.2)

</div>
