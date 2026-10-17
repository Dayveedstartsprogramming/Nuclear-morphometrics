# Nuclear Morphometrics: Benign vs. Malignant Breast Tumors

This project treats nuclear size, shape, and texture as quantitative phenotypes and tests whether they distinguish benign from malignant breast tumor samples. It combines exploratory analysis, PCA, statistical testing with multiple-testing correction, and classification models with feature importance.

[Open in Colab](https://colab.research.google.com/github/YOUR-USERNAME/nuclear-morphometrics/blob/main/analysis.ipynb)

## Dataset

Breast Cancer Wisconsin (Diagnostic) dataset (569 samples: 212 malignant, 357 benign), loaded from scikit-learn. Originally from the UCI Machine Learning Repository (Wolberg, Street & Mangasarian). Each sample has 30 features computed from digitized images of fine-needle aspirates: 10 nuclear measurements (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension), each reported as a mean, standard error, and "worst" value.

## Methods

1. Exploratory analysis: class balance, feature distributions by diagnosis, correlation heatmap
2. PCA on standardized features
3. Mann-Whitney U tests on all 30 features with Benjamini-Hochberg FDR correction and rank-biserial effect sizes
4. Logistic regression and random forest classifiers (stratified 75/25 split, 5-fold cross-validation, scaling inside a pipeline to avoid data leakage)
5. Feature importance: standardized logistic coefficients, random forest impurity importance, and permutation importance

## Key findings

- **Malignant nuclei are larger and more irregular.** The top features by effect size were worst perimeter, worst radius, worst area, and the concave-points measurements (rank-biserial effect sizes of about 0.93 to 0.95, all significant after FDR correction). For example, median worst perimeter was about 138 in malignant vs. 87 in benign samples.
- **The phenotype separates without labels.** PC1 explained about 44% of the variance and separated the two classes in an unsupervised PCA, acting as an overall "size and irregularity" axis.
- **Classification performance was high.** Logistic regression and random forest both reached a test AUC of about 0.99 and accuracy of about 97%. Malignant recall was about 91 to 92%, so roughly 1 in 12 malignant samples was missed.
- **Importance is best read at the group level.** Radius, perimeter, and area are almost perfectly correlated (r > 0.98), so the models split credit among them. The size and contour-irregularity group drives classification.

## Limitations

The dataset is small, clean, and from a single source, so near-perfect accuracy on pre-extracted measurements would not be expected to transfer to messy real-world images or other populations. Collinear features limit interpretation of individual feature importance, and these results show statistical association, not clinical validation of a diagnostic tool.

## How to run

Click the Colab badge above, or clone the repo and run `analysis.ipynb` locally with the packages in `requirements.txt`.# Nuclear-morphometrics
