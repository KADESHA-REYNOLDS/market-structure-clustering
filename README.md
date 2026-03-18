Data-Driven Market Structure Analysis
by Kadesha Reynolds & Mujtaba Ali
Erdős Institute — Spring 2026

1. Overview
This project investigates whether data-driven clusters of U.S. equities, derived from statistical properties of stock return correlations, align with the traditional Global Industry Classification Standard (GICS) sector labels.
Unlike supervised classification approaches (which risk circularity), this project uses a fully unsupervised pipeline:

Daily log return computation
Correlation matrix analysis
Spectral factor extraction
Low-dimensional embedding via eigenvectors
Hierarchical clustering
Evaluation via Normalized Mutual Information (NMI)
Interpretation through cluster–sector alignment

The goal is not to predict sectors, but to understand latent market structure and how stocks behave relative to one another.

2. Data

Source: Yahoo Finance API (yfinance)
Assets: 104 large-cap U.S. equities across 11 GICS sectors
Period: 2006–2026
Preprocessing:

Remove failed tickers
Forward-fill & back-fill missing data
Compute daily log returns



Log returns standardize movements and enable meaningful correlation-based analysis.

3. Exploratory Data Analysis (EDA)
We explore:
• Return Distribution
Daily log returns exhibit heavy tails and clustering around zero.
• Volatility Distribution
Stocks show wide variation in volatility, consistent with sector differences.
• Sector Composition
Bar chart confirms broad sector coverage.
• Correlation Structure

A 252‑day rolling correlation matrix reveals sector-level co-movement.
Heatmap shows clear blocks (Tech, Healthcare, Financials, etc.).
Histogram of pairwise correlations highlights spread across assets.

These analyses establish a foundation for spectral modeling.

4. Spectral Analysis
4.1 Eigenvalues
Eigenvalues quantify the strength of latent market factors in the correlation matrix.
4.2 Marčenko–Pastur Bound
Used to distinguish meaningful structure from noise — a standard technique in quantitative finance.
4.3 Eigenvectors
Eigenvectors represent latent market directions (factors), such as:

Overall market movement
Tech-driven behavior
Defensive vs. cyclical dynamics

This analysis identifies the most informative dimensions of stock co-movement.

5. Spectral Embedding
We construct a 3-dimensional embedding using the top eigenvectors (EV1–EV3):
E=[EV1,EV2,EV3]E = [EV1, EV2, EV3]E=[EV1,EV2,EV3]
In this reduced space:

Stocks with similar return behavior appear near each other
Natural grouping patterns become visible
This embedding becomes the basis for clustering


6. Clustering
We apply hierarchical clustering (Ward linkage) to the spectral embedding.

k = 8 clusters
Clusters vary from pure-sector groups to cross-sector mixtures
Visualizations include label-based scatterplots and cluster-colored embeddings

Clusters reveal real market themes such as:

Pure Technology cluster
Dominant Healthcare cluster
Cyclical clusters mixing Financials + Industrials
Defensive clusters mixing Utilities + Staples


7. Unsupervised Evaluation (NMI)
To avoid circularity, we evaluate cluster quality using Normalized Mutual Information (NMI).
✔ NMI compares:

Unsupervised spectral clusters, and
Known GICS sector labels

✔ NMI ranges from:

0 → no similarity
1 → perfect alignment

⭐ Our NMI = 0.527
This reflects moderate alignment, meaning:

Some clusters strongly correspond to sectors (e.g., Tech and Healthcare)
Others capture broader factor exposures (e.g., Defensive, Cyclical)

Cluster × Sector Table
We compute a crosstab showing the distribution of sectors within each cluster, confirming:

Pure clusters (e.g., Technology)
Mixed clusters reflecting multi-factor behavior


8. Interpretation
Key insights:

Traditional GICS sectors do not perfectly explain return co-movement.
Data-driven clusters reveal latent factors that go beyond sector definitions.
Behavioral (functional) groupings emerge naturally:

Defensive clusters (Staples + Utilities)
Cyclical clusters (Financials + Industrials)


Spectral clustering highlights economic relationships, not just categories.

The NMI of 0.527 quantitatively confirms that clusters partially—but not perfectly—align with sector labels.
This is expected because stock behavior is driven by many overlapping forces, not just industry classification.

9. Future Work
Potential project extensions include:

Increasing embedding dimensionality (more eigenvectors)
Trying nonlinear embeddings (t-SNE, UMAP)
Varying the number of clusters (k optimization)
Studying time-varying cluster behavior
Adding macroeconomic or factor-model features


10. How to Run the Notebook


Install required packages:
Shellpip install yfinance seaborn scipy scikit-learn matplotlib pandasShow more lines


Open the notebook in Google Colab or Jupyter.


Run sections in order:

Data Loading
EDA
Correlation Analysis
Spectral Analysis
Spectral Embedding
Hierarchical Clustering
NMI Evaluation
Interpretation



The notebook automatically saves outputs to:

results/embedding.csv
results/clusters.csv
