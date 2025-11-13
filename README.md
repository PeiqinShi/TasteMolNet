# TasteMolNet
The project used to predict sweet and bitter compounds in food and developed an online prediction tool: TasteMolNet (http://www.bstchem.fun/).
<img width="865" height="415" alt="image" src="https://github.com/user-attachments/assets/2c576315-9e9d-4a06-bfd1-5d7a3af6f558" />

# BitterSweetTasteless

This project consolidates multi-source data for bitter, sweet, and tasteless compounds, and evaluates a range of machine learning and graph neural network models for taste-property prediction and visualization. The repository is Notebook-centric, covering data cleaning, feature engineering, model training, and result analysis to support reproducibility and follow-up research.

## Repository Structure

- `data/`: Raw and processed molecular datasets, fingerprint files, and exploratory notebooks.
- `model/`: Model development notebooks and intermediate artifacts grouped by algorithm family:
  - Subfolders such as `Attentivefp/`, `MPNN/`, `GBDT/`, `rf/`, `svm/`, and `xgb/` contain training scripts using different feature sets (RDKit descriptors, MACCS, ECFP, graph features, etc.).
  - `final model.ipynb`: Comparative summary of model performance.
  - Files like `BST.csv` within subfolders store dataset splits or feature snapshots used in experiments.

## Environment Setup

Create an isolated Conda environment (Python ≥ 3.9 recommended). The following commands cover the core dependencies; adjust according to the imports used in each notebook.

```bash
conda create -n bittersweet python=3.8
conda activate bittersweet

# Core scientific stack
conda install -c conda-forge pandas numpy scikit-learn matplotlib seaborn jupyterlab

# Cheminformatics and graph models
conda install -c conda-forge rdkit=2023.09.1
conda install -c conda-forge deepchem=2.7.1
conda install -c pytorch pytorch torchvision torchaudio cpuonly

# Additional utilities
conda install -c conda-forge xgboost lightgbm openpyxl tqdm
```

> **Notes**
> - Install `deepchem` and `rdkit` via Conda to avoid binary compatibility issues.
> - For GPU acceleration, replace the PyTorch command with the CUDA build matching your hardware.
> - Some notebooks may warn about missing optional dependencies (e.g., `tensorflow`, `pytorch_lightning`). Install them only if you plan to run the corresponding models.

## Data Preparation

1. Place all source data under `data/`, including files such as `BST.csv`, `food_Compound.csv`, and `fingerprints.pkl`.
2. Datasets typically provide `SMILES` strings and multi-label `Label` columns; notebooks further split them into train/validation sets.
3. Update notebook file paths if your data resides elsewhere or has different naming.

## Notebook Workflow

1. Launch JupyterLab:
   ```bash
   conda activate bittersweet
   jupyter lab
   ```
2. Run notebooks as needed:
   - `data/data_processing.ipynb`: Data cleaning, standardization, and fingerprint generation.
   - `data/data_analysis.ipynb`, `data/Application domain.ipynb`: Exploratory analysis and applicability domain assessment.
   - `model/<model_name>/*.ipynb`: Training scripts for each algorithm/feature combination, including random vs. scaffold splits.
   - `model/final model.ipynb`: Aggregated metrics and visualizations.
3. Review the introductory cells in each notebook for input/output expectations and configurable parameters before executing.

## Results and Visualization

- Model notebooks report metrics such as accuracy, F1, precision, recall, and confusion matrices.
- `model/bittersweet/` holds publication-ready plots (PDF, TIFF, PNG).
- `model/result_*.csv` files capture prediction outputs for internal or external validation sets.

## Troubleshooting

- **DeepChem warnings**: Messages like “Skipped loading ... missing dependency” indicate optional modules that are safe to ignore unless required.
- **Chinese encodings**: Some CSV files use `gb18030` or `gb2312`; specify the encoding when loading them.
- **Relative paths**: Notebooks reference data via relative paths (e.g., `../../data/BST.csv`). Update paths if you reorganize folders.

## Recommended Next Steps

- Consolidate the best hyperparameters and results, then script the training pipeline for automation.
- Refactor recurring preprocessing steps into reusable Python modules.
- Add unit tests or minimal examples to validate data processing and prediction reliability.

Feel free to extend the dependency list or share specific error messages if you encounter issues while reproducing the experiments; contributions that improve documentation are welcome.


