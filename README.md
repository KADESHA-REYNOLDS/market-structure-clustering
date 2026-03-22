Data-Driven Market Structure Analysis

by Kadesha Reynolds & Mujtaba Ali

Erdős Institute — Spring 2026

    1. Overview
This project uncovers behavior‑based market structure in U.S. equities using an entirely unsupervised analytical pipeline. Rather than assuming that traditional sector labels explain market behavior, we let the data reveal how stocks truly move together.
Using daily log returns from 104 U.S. large‑cap stocks (2006–2026), we:

  -study co‑movement through return correlations,
  
  -extract hidden patterns using spectral analysis,
  
  -embed stocks in a low‑dimensional space using leading eigenvectors,
  
  -apply hierarchical clustering (Ward linkage), and
  
  -evaluate alignment with known GICS sectors using Normalized Mutual Information (NMI).

Our goal is not prediction, but insight:
to understand latent economic structure that drives stock behavior.


    2. Stakeholders & Practical Use
This analysis is valuable for:

  -Portfolio Managers — reveal hidden correlations and improve diversification
  
  -Risk Management Teams — detect groups of stocks that move together to reduce portfolio volatility
  
  -Quant Funds & Algorithmic Traders — use behavior-based clusters for factor-aware strategies
  
  -Individual Traders — understand which stocks tend to move together during earnings or macro events

Value-add: Clusters show defensive, cyclical, and other cross‑sector behavioral groups that sector labels alone cannot capture.


    3. Data


Source: Yahoo Finance API (yfinance)

Assets: 104 large-cap U.S. equities across 11 sectors

Period: 2006–2026

Transformations:

Forward-fill + back-fill missing values
Daily log returns



Daily returns standardize stock movements and make correlation-based analysis meaningful.


    4. Exploratory Analysis (High-Level Summary)
We performed a brief EDA including:

  -Return distribution: mostly centered around zero with heavy tails
  
  -Volatility distribution: varied across sectors, indicating different risk profiles
  
  -Correlation heatmap: clear blocks by sector, plus cross-sector relationships (shared factors)

These insights motivated the use of spectral analysis to uncover deeper structure.

    5. Spectral Analysis
We analyze the correlation matrix via:

  Eigenvalues: identify dominant market factors
  
  Marčenko–Pastur bound: separate meaningful structure from noise
  
  Eigenvectors: reveal hidden behavioral patterns not visible in raw correlations

The top eigenvectors form a 3D spectral embedding representing the main dimensions of co‑movement.

    6. Clustering
Using the spectral embedding, we apply hierarchical clustering (Ward linkage):

  k = 8 clusters
  
  Reveals sector‑pure groups (Technology, Healthcare)
  
  Reveals mixed groups representing economic behaviors:
    Defensive: Utilities + Staples
    Cyclical: Financials + Industrials



Clusters reflect how stocks behave, not how sectors label them.

    7. KPI: Unsupervised Evaluation Using NMI
Our key performance indicator (KPI) is: Normalized Mutual Information (NMI)

NMI measures how similar two sets of labels are, without requiring a predictive model.
  0 → no alignment
  1 → perfect alignment

Our score: NMI = 0.527

This indicates moderate alignment between cluster structure and sector labels — suggesting clusters capture deeper economic factors beyond sector categories.

A cluster–sector contingency table further highlights:
  -strong matches for Technology & Healthcare
  -cross‑sector clusters driven by macroeconomic exposures


    8. Interpretation

The market is inherently multi‑factor:
  -broad market risk
  
  -interest-rate sensitivity
  
  -defensive vs cyclical behavior
  
  -sector-specific patterns

Therefore, clustering reveals behavioral market structure:
  
  -Pure clusters represent sectors with strong internal cohesion
  
  -Mixed clusters represent shared economic exposures

This provides richer insight than sector classifications alone.

    9. Future Work
Potential extensions:
  
  -Use more eigenvectors for higher-dimensional embeddings
  
  -Apply nonlinear techniques (UMAP, t‑SNE)
  
  -Explore time‑varying clusters across market regimes
  
  -Incorporate macroeconomic factors

    10. How to Run This Project

1. Install dependencies:
     pip install yfinance seaborn scipy scikit-learn matplotlib pandas

2. Run project_erdos.ipynb or the Python script version.

3. Outputs saved automatically:
    results/embedding.csv
    results/clusters.csv

These support reproducibility and downstream analysis.

