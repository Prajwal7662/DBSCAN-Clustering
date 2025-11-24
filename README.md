# DBSCAN Clustering — README 🚀

**Notebook:** `/mnt/data/DBSCAN_Clustering.ipynb`

## Project overview 📌

This notebook demonstrates DBSCAN (Density-Based Spatial Clustering of Applications with Noise) on a dataset, covering data loading and preprocessing, parameter selection (eps, min_samples), k-distance plot analysis, clustering execution, outlier detection, evaluation, and visualization.

It is written as an interactive Jupyter Notebook and intended for students or practitioners exploring density-based clustering and outlier detection.

---

## Contents / sections (in the notebook) 📂

1. **Introduction & objective** — what DBSCAN is, strengths (identifies clusters of arbitrary shape, handles noise) and when to use it.
2. **Imports & environment** — required Python packages.
3. **Load dataset** — CSV, sklearn datasets, or synthetic data (make_moons, make_blobs) examples.
4. **Preprocessing** — scaling (StandardScaler), handling missing values, optionally PCA for visualization.
5. **k-distance plot** — compute nearest-neighbor distances to choose `eps` visually.
6. **DBSCAN fit** — run `sklearn.cluster.DBSCAN` with chosen `eps` and `min_samples` and inspect `labels_` (noise labeled `-1`).
7. **Evaluation** — silhouette score (only on non-noise points), cluster counts, number of noise points, and simple cluster statistics.
8. **Visualization** — 2D scatter plots (PCA/t-SNE) colored by cluster label with noise highlighted; density plots where helpful.
9. **Sensitivity analysis** — vary `eps` and `min_samples` to show how clusters and noise change.
10. **Conclusions & notes** — observations, limitations, and suggestions for further work.

---

## Requirements 📦

Same base packages as typical clustering projects. Example `requirements.txt` entries:

```
numpy
pandas
scikit-learn
scipy
matplotlib
seaborn
jupyter
plotly   # optional
```

Install with:

```bash
python -m venv venv
source venv/bin/activate   # on Windows: venv\Scripts\activate
pip install -r requirements.txt
```

---

## How to run ▶️

1. Open the notebook in Jupyter Lab / Notebook:

```bash
jupyter lab /mnt/data/DBSCAN_Clustering.ipynb
# or
jupyter notebook /mnt/data/DBSCAN_Clustering.ipynb
```

2. Run the cells sequentially. The notebook includes helper cells to compute k-distance plots and to run batch parameter sweeps.

3. To save cluster assignments to CSV:

```python
# inside notebook
df['dbscan_label'] = labels
df.to_csv('dbscan_clusters.csv', index=False)
```

---

## Typical parameters you may change ⚙️

* `eps` (epsilon): neighborhood radius; choose using k-distance plot (elbow point).
* `min_samples`: minimum samples in neighborhood to form a core point (often `dim + 1` or 4–10 for low-dim data).
* `metric`: distance metric (default `'euclidean'`); consider `'manhattan'` or `'cosine'` depending on data.
* scaling: always scale features when using Euclidean distance.

---

## Expected outputs / artifacts 📤

* Cluster labels with noise indicated by `-1`.
* k-distance plot(s) used to choose `eps`.
* Counts for each cluster and number of noise points.
* Visual plots showing clusters and noise.
* Optionally: `dbscan_clusters.csv` containing original data + `dbscan_label`.

---

## Tips & suggestions 💡

* Always scale numeric features before DBSCAN when using Euclidean distance.
* Use the k-distance plot (k = `min_samples`) and look for the elbow to guide `eps` choice.
* For high-dimensional data, consider dimensionality reduction (PCA, UMAP) before clustering or use alternate metrics.
* DBSCAN’s runtime scales roughly O(N log N) with a good spatial index (e.g., KD-Tree) but can be slower for high dimensionality.
* If clusters have varying density, consider HDBSCAN (hierarchical density-based clustering) which handles variable density better.

---

## Troubleshooting 🛠️

* **All points labeled noise:** increase `eps` or decrease `min_samples` and check scaling.
* **Single big cluster:** decrease `eps` or increase `min_samples` to split.
* **Optimal `eps` unclear:** try parameter sweeps and visualize results, or use silhouette on non-noise points for guidance.

---

## Reproducibility 🔁

* Fix seeds when generating synthetic datasets.
* Save `eps` and `min_samples` values used for experiments.

---

## Attribution / Author

Prepared for: **Prajwal Mavkar**.
Notebook path: `/mnt/data/DBSCAN_Clustering.ipynb`.

---

## License

MIT License — feel free to reuse for coursework or projects; please credit the original author when reusing substantial portions.

---

## Next steps (optional) ➡️

* Generate a `requirements.txt` based on imports in this notebook.
* Create a `run_dbscan.py` script to run parameter sweeps and save outputs.
* Convert notebook into a short README + example script for reproducible experiments.

*If you want, I can generate the `requirements.txt` and `run_dbscan.py` now.*
