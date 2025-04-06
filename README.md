# Predictive modeling of cancer multi-omic datasets

In this repository, I build variational autoencoder (VAE) inspired models to predict drug response from multi-omic datasets for 175 lung cancer cell lines.

## Biological question and rationale for modeling

Modern genomics approaches allow us to get detailed insight into several cellular phenotypes such as chromatin accessibility, transcript levels, protein abundance, among others. How these phenotypes map to 1) drug response or 2) gene essentiality are very relevant from a therapeutic / drug development standpoint. For instance, if we had a model trained on vast omics datasets, we could answer questions like:

- can we identify promising drug candidates for cell lines with omics data but limited drug response measurements?
- alteratively, can we identify conditionally essential genes as preliminary targets for therapeutic development?

In this modeling problem, I will focus on predicting drug response from three measurement types: transcriptomics, proteomics, and methylation.

## Modeling framework

I will apply a VAE framework (with an encoder and decoder), typically used to reconstruct inputs and learn embeddings, to instead predict drug response. The intuition behind this is that model training maps input omics datasets to drug response through a latent space representation. I decided to use a VAE instead of a transformer because:
- the probabilistic representation of inputs in VAEs can help prevent overfitting through latent space regularization
- VAEs are much faster to train than transformer based models
- there's only 175 cancer cell models, and a large transformer model could overfit to the limited data

### Validating model predictions
- I performed 5-fold cross validation of the lung cancer datasets, and assessed model performance of drug response prediction on the training vs validation datasets.
- I trained the model on all 175 lung cancer cell lines, and predicted drug response for 46 skin cancer cell lines, to assess generalizability of the model across cancer types.

## Installation and usage

- Clone the github repository 
- Navigate to the cloned repository path and download the multi-omic datasets from the following [link](https://drive.google.com/drive/folders/1g4g20a6_SSmhshHjEEEf0xT3rpq3vrG4). The directory structure should look as follows:

    ``` 
    local_path/cancer_multiome
    │   README.md
    │   LICENSE    
    │   data_exploration.ipynb
    │   vae_predictive_model.ipynb
    └───Dataset
        └───Lung
            │   20231023_092657_fusions_latest.csv
            │   20231023_092657_imputed_copynumber.csv
            │   ...
        └───Skin
            │   20231023_092657_fusions_latest.csv
            │   20231023_092657_imputed_copynumber.csv
            │   ...       
    ```

- Create a conda environment with required packages:  `conda env create -f torch_env.yaml`
- Activate the conda environment: `conda activate torch_env`
- Launch JupyterLab and run the `vae_predictive_model.ipynb` notebook.
    - Model training and inference on MacBook Air M1 (8GB CPU)
    - 400 epochs for lung cancer dataset model training took ~30 seconds
    
## Misc notes:

- Time taken to build and run the code: ~5 hours
- Total time for completion (including writeup, code organization): ~7 hours
