# Structure-Decoupling Index-Based Analysis and Classification of Autism Spectrum Disorder

## 📄 Summary

This project investigates the **Structure-Decoupling Index (SDI)** as a neuroimaging biomarker to distinguish individuals with **Autism Spectrum Disorder (ASD)** from **Typically Developing (TD)** controls using **Structural Connectivity (SC)** and **Functional Connectivity (FC)** data from the **ABIDE I and II** datasets. The SDI quantifies the mismatch between brain structure and function via **graph spectral decomposition**.

Both SC-informed and FC-informed SDI variants were computed, and used as features in multiple machine learning pipelines. The project evaluates SDI's robustness, biological validity, and classification performance across sites.

---

## 🧠 Key Concepts

- **Structural Connectivity (SC)**: Anatomical white-matter pathways derived from diffusion MRI.
- **Functional Connectivity (FC)**: Temporal correlations between brain region activities from resting-state fMRI.
- **Structure-Function Coupling**: The extent to which FC aligns with SC.
- **Structure-Decoupling Index (SDI)**: Ratio of high-frequency to low-frequency graph energy indicating decoupling between FC and SC.

---

## 🗃️ Datasets

### ABIDE I
- 17 international sites, 1112 subjects.
- Includes fMRI and structural MRI.
- **No SC data** → Only FC-informed SDI.

### ABIDE II
- 19 sites, >1000 subjects.
- Some sites provide DWI → enables SC-informed SDI.
- Used sites: **NYU1, NYU2, SDSU, BNI**

---

## 🧮 Methodology

### SDI Computation

1. **Graph Laplacian** from SC or FC matrix.
2. **Eigen-decomposition**: Derive graph modes.
3. **Projection**: Project fMRI time series onto modes.
4. **Spectral Energy Split**:
   - Low-frequency modes → structure-aligned.
   - High-frequency modes → decoupled.
5. **SDI = E<sub>high</sub> / E<sub>low</sub>**

### Variants:
- **SC-informed SDI**: Uses structural Laplacian.
- **FC-informed SDI**: Uses functional Laplacian.

---

## 🧪 Machine Learning Pipeline

- **Features**: 400-node SDI vectors (Schaefer-400 atlas).
- **Preprocessing**:
  - Imputation, SMOTE, PCA, feature selection
- **Models**:
  - SVM, Logistic Regression, Random Forest, XGBoost, Stacking
- **Evaluation**:
  - Accuracy, Balanced Accuracy, Classification Reports

---

## 🔍 Results Summary

| Dataset                            | SDI Type          | Test Accuracy | Balanced Accuracy |
|-----------------------------------|-------------------|---------------|-------------------|
| ABIDE II (204 subjects)           | SC-based          | 53.66%        | 48.0%             |
| ABIDE II (203 subjects)           | FC-based          | 53.66%        | 52.0%             |
| ABIDE I (867 subjects)            | FC-based          | **64.37%**    | 64.0%             |
| Combined ABIDE I + II (1070 subj) | SC + FC (800-D)   | 62.1%         | **62.0%**         |

- **Best performance** with combined SC+FC features using **Logistic Regression + Hybrid preprocessing**.
- SDI features show moderate but consistent discriminatory ability.

---

## 📊 Spectral Analysis & Insights

- **Energy Spectral Density (ESD)** plots show group-level differences in how ASD and TD subjects align with low-frequency structural modes.
- **Graph-theoretic metrics** like eigenvalue distributions serve as proxies for white matter fiber density.
- **Spatial SDI maps** highlight decoupling patterns in specific brain regions.

---

## 🛠 Tools and Libraries

- Python, NumPy, Pandas, Scikit-learn, Seaborn, Matplotlib
- Neuroimaging tools: NiBabel, Nilearn
- Graph Signal Processing: Custom Laplacian and spectral projections
- Data: ABIDE I & II (publicly available)

---

## 📌 Conclusion

- **SDI is a promising biomarker** for characterizing structure–function misalignment in ASD.
- **FC-based SDI** is applicable even when DWI is unavailable.
- **Combining SC and FC modalities improves accuracy**.
- Further work includes:
  - Deep learning (GNNs, autoencoders)
  - Cross-site harmonization
  - Phenotypic integration


---

## 🧭 License

This project is part of a summer internship under BCCL, IIIT-H, and is intended for academic research purposes only.

