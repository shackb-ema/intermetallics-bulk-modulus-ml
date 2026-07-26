# Data Directory

This folder holds the processed CSV datasets used by the notebooks in this repository. Raw data itself comes from the [Materials Project](https://materialsproject.org/) API (an external source) and is queried live in `notebooks/01_data_acquisition.ipynb`; it is not committed here if the resulting file exceeds 50MB (see the repository `.gitignore`).

## Files

- `bradley_intermetallics_elasticity.csv`: Raw-ish output of `01_data_acquisition.ipynb`. One row per Materials Project entry that passed the binary/ternary transition-metal intermetallic filters, with columns `material_id`, `formula`, `bulk_modulus_vrh` (GPa, target variable), `crystal_system`, `elements`, and `num_elements`. Unphysical bulk modulus values (outside 0-1000 GPa) have already been dropped.
- `bradley_intermetallics_featured.csv`: Output of `02_eda_featurization.ipynb`. Adds 132 MAGPIE composition descriptors, one-hot encoded crystal-system columns (`cs_*`), the valence electron concentration (`VEC`), and the `chem_system` group key (sorted element symbols joined by a hyphen) used for grouped cross-validation and train/test splitting in `03_modeling.ipynb` and `04_results_visualization.ipynb`.

## Regenerating

Both files can be regenerated from scratch by running `01_data_acquisition.ipynb` followed by `02_eda_featurization.ipynb`, provided a valid `MP_API_KEY` is set in a `.env` file at the repository root.
