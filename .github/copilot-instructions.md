<!--
Short, actionable instructions for AI coding agents working on this repo.
Keep this file concise (20–50 lines) and focused on repository-specific patterns.
-->
# Guidance for AI coding agents

Purpose
- This repository is a Jupyter notebook exercise ( `lab5.ipynb` ) about Gaussian Mixture Models (GMMs).
  The goal for contributors is to implement TODO cells inside the notebook (data generation, E-step/M-step, training loop) and ensure visualizations run correctly.

Quick start (what a human developer would do)
- Use Python 3.8+ in a virtual environment. The notebook imports indicate these runtime deps: numpy, scipy, pandas, matplotlib, seaborn, scikit-learn.
- Typical setup commands (for humans working locally):
  - python -m venv .venv
  - .venv\Scripts\Activate.ps1   (PowerShell on Windows)
  - pip install numpy scipy pandas matplotlib seaborn scikit-learn
  - Open `lab5.ipynb` in VS Code or Jupyter and run cells.

Files of interest
- `lab5.ipynb` — single notebook containing all exercises and the code to implement. Focus edits here.
- `README.md` — short assignment note (no build/CI config exists).

Project-specific patterns and expectations
- Notebook-driven development: implement TODOs in cells (search for lines beginning with `# ----------------------------` and `# TODO`).
- Naming conventions the notebook expects:
  - 1D/2D sample variables: `data1`, `data2`, `data3` (NumPy arrays; 1D or 2D as appropriate).
  - Dataset stack: `X = np.vstack([data1, data2, data3])` (shape (N, D)).
  - Initialization outputs: `means_init`, `covs_init`, `weights_init` used later by training/visualization.
  - EM functions: `e_step(X, means, covariances, weights)` should return responsibilities array of shape (N, K).
  - `m_step(X, resp)` should return (means, covariances, weights) where `means` is (K, D), `covariances` is a list of K (D x D) arrays, and `weights` is length-K vector.

API / library usage seen in the notebook
- Use `np.random.normal` and `np.random.multivariate_normal` for sampling.
- Use `scipy.stats.multivariate_normal.pdf` or `scipy.stats.multivariate_normal(mean, cov).pdf(pos)` for pdf calculations in E-step / plotting.
- Use `scipy.stats.norm.pdf` for 1D PDF plotting in Exercise 5.
- Visualization style: seaborn.kdeplot for KDE/contours, matplotlib 3D axes (mpl_toolkits.mplot3d) for surfaces.

Important implementation hints (derived from notebook)
- Keep random seeds deterministic where the notebook does (e.g., `np.random.seed(42)`) so visualizations are stable.
- When computing responsibilities, multiply each component's PDF by its weight before normalizing across components.
- In M-step, compute Nk = resp.sum(axis=0), update mean as np.dot(resp.T, X) / Nk[:, None], covariances as weighted outer-products divided by Nk[k].
- Shapes matter: validate shapes before returning (N, D), (K, D), list of K (D x D), and weights sum to 1.

What not to change
- Do not rename the major variables the rest of the notebook expects (data1/2/3, means_init, covs_init, weights_init, X). Changing cell ids is unnecessary and not helpful.

Testing and verification
- Run the notebook end-to-end. Visual checks (KDE plots, 3D surfaces, training visualization) are the primary verification method here.
- There is no automated test suite or CI in this repo.

When to ask the human
- If you need to add new files (requirements.txt, scripts) or change the notebook structure significantly, request confirmation from the repo owner.

If anything in this document looks incomplete, tell me which part to expand or which cells you want me to inspect/modify next.
