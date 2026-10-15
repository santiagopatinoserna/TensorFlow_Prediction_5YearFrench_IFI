# French IFI tax: regression model comparison

An exploratory comparison of regression models for municipal IFI tax totals, using past tax records and geographic features.

## What is implemented

[Model-selection notebook](Script/Model_selection_ML_NN.ipynb):

- Load the bundled Excel files, clean commune identifiers and join coordinates.
- Build lagged tax values, prior-history statistics and a nearest-commune distance feature.
- Compare linear regression, decision trees, random forest, XGBoost and a TensorFlow neural network, with tuning experiments and cross-validation.
- Export cleaned tables, model inputs and charts in `Dataout/`.
- Include an OpenAI-based interpretation section. This is not an independent validation of the chosen model.

## Important limitations

- The notebook fits scaling before a random train/test split. Preprocessing therefore sees held-out data.
- A random row split and K-fold evaluation are not a historical, forward-only forecast test. Records from a commune can appear on both sides of the split.
- Published scores should not be treated as evidence of future-year accuracy or a production-ready forecast.
- A proper follow-up needs chronological backtesting, fold-local preprocessing and comparison with a last-observed-value baseline.

## Reproduction notes

This notebook was written for Google Colab. It mounts Drive and uses absolute `/content/drive/...` paths. Update `DATA_PATH`, `PATH_IN` and `PATH_OUT` to your checkout before running it. Local execution also requires removing or adapting the Colab-only mounting cell.

Imports include pandas, NumPy, scikit-learn, XGBoost, TensorFlow, Keras Tuner, matplotlib, seaborn, Plotly and the OpenAI SDK. Reading the mixed Excel inputs also needs compatible Excel readers. The original environment is not locked; installing current versions is not a verified reproduction recipe. Review the OpenAI section before executing it: external calls may incur costs and should not receive private data.

## Saved artifacts

![XGBoost diagnostic from the original experiment](Dataout/XGBoost%20%28Grid%20Search%29%20IFI_TAX.png)

See `Dataout/df_to_model.csv` and the other tables for the saved model inputs. Charts above are historical outputs, not a fresh benchmark.

## Project status

Historical exploratory work using the 2019 to 2022 IFI input files kept in `DataIn/`. This is a research notebook, not a deployed service. The notebooks and exported results have not been rerun end to end in the current environment.

## Data and reuse

The tax input files are attributed in the project notebooks to the French public dataset *Impôt de solidarité sur la fortune / Impôt sur la fortune immobilière par collectivité territoriale*. Commune coordinates and lookup tables are included in `DataIn/`. Source files and derived tables retain their applicable upstream terms; this repository does not grant a new licence over those datasets. Check the original publisher and the terms for each input before redistribution.

## Author

Santiago Patiño Serna. [LinkedIn](https://www.linkedin.com/in/santiago-patino/) · [Godi.AI](https://godi.ai).
