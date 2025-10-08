## Multimodal Deep Learning for Opportunistic Osteoporosis Screening Using Knee X-rays and Clinical Risk Factors
> This project explores opportunistic osteoporosis screening from knee X-rays, using multimodal deep learning to identify low bone density in routine orthopedic radiographs by combining imaging biomarkers with clinical risk factors to enable early detection without additional radiation or cost.
> 
> 
> ![btnh small](https://github.com/user-attachments/assets/6c4017eb-12c0-40c3-af35-3c499a5445a4) \
> bone (knee x-ray) + tags (clinical metadata) --> harmony (multimodal fusion to predict BMD) \
> _BMD - bone mineral density_

### Motivation

Osteoporosis is often underdiagnosed because patients rarely undergo dedicated bone mineral density (BMD) scans until a fracture occurs. However, many adults undergo knee X-rays for other reasons, such as orthopedic complaints or arthritis assessment. These X-rays, combined with simple clinical data, could potentialy serve as a source for _opportunistic osteoporosis screening_, detecting low bone density early and prompting preventive care.  

#### Clinical Impact
- Enables early identification of patients at risk for osteoporosis using **already available knee X-rays**, reducing the need for additional tests  
- Supports **preventive care and fracture risk reduction**  
- Demonstrates the value of **multimodal AI in enhancing routine imaging workflows**

### Objective(s)
Develop a multimodal deep learning model that integrates:
1) Knee X-ray images
2) Clinical metadata & lifestyle risk factors
   > eg. age, sex, menopause age, diabetes, smoking, etc.

to classify patients according to bone health status.

The initial task will be **binary classification**: Normal BMD vs Low BMD (Osteopenia + Osteoporosis). After establishing a reliable binary model, we plan on extending the framework to a **3-class** classification model: Normal, Osteopenia, Osteoporosis. This proposed staged approach addresses class imbalance while retaining clinical relevance.

### Data
https://data.mendeley.com/datasets/fxjm8fb6mw/2
- **Images:** Knee X-rays from the Mendeley Osteoporosis dataset (total 239 images; Normal: 36, Osteopenia: 154, Osteoporosis: 49)  
- **Tabular features:** Clinical, demographic, lifestyle, and nutritional information, including T-score and diagnosis labels from the accompanying Excel sheet

Each image is mapped to tabular data via unique subject IDs (data is linked). \
Can consider finding additional datasets for further testing.

### Methods

1. **Data Preprocessing**
   - Image preprocessing: resize, normalize, and augment (rotation, horizontal flips)
   - Tabular features: encode categorical variables, standardize numeric variables, handle missing values  

2. **Model architecture**
   - **Image encoder:** Pretrained CNN (DenseNet-121 / ResNet) to extract visual features from knee X-rays  
   - **Tabular encoder:** Feed-forward MLP for clinical/lifestyle features  
   - **Fusion layer:** Concatenate image and tabular embeddings, followed by fully connected layers to predict class probabilities

3. **Training**
   - Loss: Class-weighted cross-entropy for binary classification  
   - Optimization: Adam with weight decay and early stopping  
   - Data handling: Stratified train/val/test split, optional k-fold cross-validation, and class-balanced sampling to mitigate imbalance

4. **Evaluation**
   - Metrics _(to be finalized)_
     - AUROC
     - AUPRC
     - sensitivity/recall
     - accuracy
     - confusion matrix  
   - Ablation
     - image-only
     - tabular-only
     - fused multimodal
   <!-- [time permitting:] Explainability: Grad-CAM for image contributions, SHAP/permutation importance for tabular features -->

### Expected outcomes
- _Reasonably accurate_ bone mineral density 3-way classification using opportunistic osteoporosis screening from routine knee X-rays
- Demonstrate that multimodal fusion _improves_ prediction over image-only or tabular-only models  
- Visual and tabular _feature insights_ <!-- expand on this? -->

### Timeline

| Phase | Goals |
|-------|------------|
| Phase 1 | Data cleaning, manifest creation, image/tabular preprocessing |
| Phase 2 | Implement and train binary classifier (Normal vs Low BMD), evaluate performance |
| Phase 3 | Extend to 3-class classification (Normal vs Osteopenia vs Osteoporosis) <!--T-score regression?--> |
| Phase 4 | Evaluate final performance, run ablation study |
| Phase 5 | Compile results & visualization for report & presentation |
