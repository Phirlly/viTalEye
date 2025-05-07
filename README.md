
# 👁️‍🗨️ ViTal-Eye: Transformer-Driven Retina Screening

*Lightweight, Interpretable, and Robust Diabetic Retinopathy Detection with Vision Transformers*

---

## 📌 Overview

**ViTal-Eye** is an exploratory AI-based diagnostic system for **automated diabetic retinopathy (DR) screening** using Vision Transformers (ViTs). Developed as a course project for *ECEN 642 - Digital Image Processing & Computer Vision*, this study benchmarks a **ViT-Base/16** against a **ResNet-50** backbone, showcasing how self-attention can elevate clinical interpretability and robustness in real-world medical imaging.

> **Goal**: Build a fast, scalable, and explainable “second reader” for DR screening in resource-limited settings.

---

## 🧠 Key Features

- 🔍 **ViT-Base/16 Backbone**: Global self-attention and transparent attention rollout for feature interpretation.
- 🧠 **ResNet-50 Baseline**: Strong CNN comparator with Grad-CAM interpretability.
- 📊 **Robust Evaluation**: Accuracy, AUC, quadratic-weighted κ, sensitivity@95% specificity.
- 🌫️ **Stress Tested**: Performs under blur and brightness distortions.
- 📈 **Efficient Training**: Competitive accuracy in <1 hour on a single GPU.

---

## 📚 Dataset Details

Two public datasets were used:

- **EyePACS** (Kaggle 2015): ~35,000 fundus images across 5 DR severity levels.
- **APTOS 2019**: 3,662 annotated images with identical DR grading scale.

All images were center-cropped, normalized, and augmented for robustness.

---

## ⚙️ Methodology

### 🔄 Data Processing

- Center crop, resize (512×512), normalize
- Augmentations: flips, rotation, brightness/contrast jitter, CLAHE, Gaussian blur

### 🏗️ Model Architectures

| Model       | Description                          |
|-------------|--------------------------------------|
| **ViT-Base**| 12-layer transformer (patch size 16) |
| **ResNet-50**| Standard CNN backbone baseline       |

- ViT is partially frozen (first 3–6 blocks) and fine-tuned
- Mixed-precision training using PyTorch Lightning + `timm` + HuggingFace

### 📉 Training

- Optimizer: `AdamW`
- Learning Rate: `3e-4` with cosine annealing
- Loss: Weighted cross-entropy
- Epochs: 15 (with early stopping)

---

## 📈 Results

### ✅ Performance (ViT)

| Metric                        | Value        |
|------------------------------|--------------|
| Test Accuracy                | 77.5%        |
| AUROC (no DR vs DR)         | 0.8203       |
| Quadratic-weighted Kappa    | 0.5399       |
| Sensitivity @ 95% Specificity | 44.99%       |

### 🔍 Robustness

| Perturbation     | ViT AUC | ResNet AUC |
|------------------|---------|------------|
| Blur (severity 1–3)   | 0.771–0.764 | ~0.001–0.002 |
| Brightness (1–3)      | 0.744       | ~0.000       |

### 🖼️ Interpretability

| Method         | Highlights                |
|----------------|---------------------------|
| **Attention Rollout** (ViT) | Clear microaneurysm/hemorrhage focus |
| **Grad-CAM** (ResNet)       | Often highlights irrelevant regions  |

---

## 🚀 Future Work

- 🔄 Semi/self-supervised ViT pretraining
- 📱 Edge-device deployment (e.g., mobile screening kits)

---

## 📜 Citation

If you use ViTal-Eye, please cite:

> Okunola, A. O. *ViTal-Eye: Transformer-Driven Retina Screening Study*. ECEN 642 – Digital Image Processing & Computer Vision. Texas A&M University, 2025.

---

## 👨‍⚕️ Acknowledgments

This work was submitted to **ECEN 642-600/700** under the supervision of **Professor Zixiang Xiong**.

---
## References
```bibtex
@book{gonzalez2018digital,
  author    = {Rafael C. Gonzalez and Richard E. Woods},
  title     = {Digital Image Processing},
  edition   = {4th},
  publisher = {Pearson},
  address   = {330 Hudson Street, New York, NY 10013},
  year      = {2018}
}

@book{umbaugh2020computer,
  author    = {Scott E. Umbaugh},
  title     = {Computer Vision and Image Analysis: Digital Image Processing and Analysis},
  edition   = {4th},
  publisher = {CRC Press},
  address   = {6000 Broken Sound Parkway NW, Suite 300, Boca Raton, FL 33487-2742},
  year      = {2020}
}

@book{horn2013matrix,
  author    = {Roger A. Horn and Charles R. Johnson},
  title     = {Matrix Analysis},
  edition   = {2nd},
  publisher = {Cambridge University Press},
  address   = {32 Avenue of the Americas, New York, NY 10013-2473, USA},
  year      = {2013}
}
@article{zheng2012worldwide,
  author  = {Y. Zheng and M. He and N. Congdon},
  title   = {The worldwide epidemic of diabetic retinopathy},
  journal = {Indian Journal of Ophthalmology},
  year    = {2012},
  volume  = {60},
  pages   = {428--431}
}

@article{etdrs1985photocoagulation,
  author  = {{Early Treatment Diabetic Retinopathy Study Research Group}},
  title   = {Photocoagulation for diabetic macular edema},
  journal = {Archives of Ophthalmology},
  volume  = {103},
  number  = {12},
  pages   = {1796--1806},
  year    = {1985}
}

@article{gulshan2016deep,
  author  = {Varun Gulshan and Lily Peng and Marc Coram and Martin C. Stumpe and Derek Wu and Arunachalam Narayanaswamy and Subhashini Venugopalan and Kasumi Widner and Tom Madams and Jorge Cuadros and others},
  title   = {Development and validation of a deep learning algorithm for detection of diabetic retinopathy in retinal fundus photographs},
  journal = {JAMA},
  volume  = {316},
  number  = {22},
  pages   = {2402--2410},
  year    = {2016}
}

@inproceedings{dosovitskiy2021image,
  author    = {Alexey Dosovitskiy and Lucas Beyer and Alexander Kolesnikov and Dirk Weissenborn and Xiaohua Zhai and Thomas Unterthiner and Mostafa Dehghani and Matthias Minderer and Georg Heigold and Sylvain Gelly and Jakob Uszkoreit and Neil Houlsby},
  title     = {An image is worth 16x16 words: Transformers for image recognition at scale},
  booktitle = {Proceedings of the International Conference on Learning Representations (ICLR)},
  year      = {2021}
}

@inproceedings{abnar2020quantifying,
  author    = {Samira Abnar and Willem Zuidema},
  title     = {Quantifying attention flow in transformers},
  booktitle = {Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics (ACL)},
  pages     = {4190--4197},
  year      = {2020}
}

@misc{eyepacs2015,
  author       = {{EyePACS}},
  title        = {Diabetic retinopathy detection challenge},
  year         = {2015},
  howpublished = {\url{https://www.kaggle.com/c/diabetic-retinopathy-detection}}
}

@misc{aptos2019,
  author       = {{APTOS}},
  title        = {Blindness detection challenge},
  year         = {2019},
  howpublished = {\url{https://www.kaggle.com/c/aptos2019-blindness-detection}}
}

@book{idf2021,
  author    = {{International Diabetes Federation}},
  title     = {IDF Diabetes Atlas},
  edition   = {10th},
  year      = {2021},
  publisher = {International Diabetes Federation}
}
@article{Abramoff2018Pivotal,
  author  = {Michael D. Abr{\`a}moff and Paul T. Lavin and Michael Birch and Naveed Reiter and James P. F. Russell},
  title   = {Pivotal Trial of an Autonomous AI-Based Diagnostic System for Detection of Diabetic Retinopathy in Primary Care Offices},
  journal = {NPJ Digital Medicine},
  year    = {2018},
  volume  = {1},
  number  = {1},
  pages   = {39},
  doi     = {10.1038/s41746-018-0040-6}
}

@article{Li2019CBAM,
  author  = {Xutao Li and Shaoan Zhu and Yu Zhang and Huazhu Fu and Jen Hong Tan and Jonathan Li},
  title   = {Attention-Guided ResNet with Convolutional Block Attention Module for Diabetic Retinopathy Grading},
  journal = {IEEE Access},
  year    = {2019},
  volume  = {7},
  pages   = {6428--6436},
  doi     = {10.1109/ACCESS.2018.2886784}
}

@misc{Chen2021TransUNet,
  author       = {Jiachen Chen and Yueming Lu and Qi Dou and Jing Qin and Pheng-Ann Heng},
  title        = {TransUNet: Transformers Make Strong Encoders for Medical Image Segmentation},
  howpublished = {arXiv preprint arXiv:2102.04306},
  year         = {2021},
  note         = {\url{https://arxiv.org/abs/2102.04306}}
}
@article{li2021swin,
  title   = {Swin transformer: Hierarchical vision transformer using shifted windows},
  author  = {Liu, Ze and Lin, Yutong and Cao, Yixuan and Hu, Han and Wei, Yixuan and Zhang, Zheng and Lin, Stephen and Guo, Baining},
  journal = {arXiv preprint arXiv:2103.14030},
  year    = {2021}
}

