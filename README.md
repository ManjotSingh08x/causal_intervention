
# Causal Intervention 
This folder contains jupyter notebooks to run code pertaining to reproducing our results for Causal Intervention in 4 Models on Python and C++ datasets. 

We also have code available for running other dataset pairs as well, such as finance-medical and science-maths pairs. They can be run by removing comments in the code at specific locations

## Table of Contents
1. [Repository Structure](#repository-structure)
2. [Setup and Installation](#setup-and-installation)
3. [Reproduction Workflow](#reproduction-workflow)

## Repository Structure

```bash
.
├── full_compute/     # Raw outputs from the intervention analysis for each model.
├── graphs/           # Directory with generated graphs and figures for each model.
├── prompt_set/       # The different sets of prompts used in the experiments.
├── scores/           # Contains the precalculated metric scores for each model's layers.
├── token_sets/       # Stores JSON files for specific token IDs and their string representations.
│
├── 01_reverse_intervention.ipynb   # Notebook for running the reverse intervention experiments.
├── 02_all_model_causal.ipynb       # Notebook for analyzing causal intervention for all models.
├── 03_graph_generator.ipynb        # Notebook to generate all plots and figures from the processed data.
├── 04_prompt_visualization.ipynb   # Notebook for visualizing the prompts and their properties.
│
├── README.md                       # The main documentation for this repository.
└── requirements.txt                # A list of all Python packages required to run the notebooks.
```

## Setup and Installation
Create a virtual environment to use in jupyter notebooks. 
```bash
python -m venv causal
```
on macOS and Linux
```bash
source causal/bin/activate
```
on Windows
```bash
source .\venv\Scripts\activate
```
install the packages 
```bash
pip install -r requirements.txt
```
Now you can easily run all jupyter notebooks in sequence to reproduce our results

## Reproduction Workflow 
The core analysis is contained in a series of Jupyter Notebooks. Please execute them in a sequential order. For each Notebook, you can run all cells by selecting **"Run"** **>** **"Run All Cells** in the Jupyter Lab/Notebook Menu. 

### 1. Reverse Intervention 
The notebook `01_reverse_intervention.ipynb` is responsible for generating token sets according to domain pairs by running intervention tests on a domain pair and seeing which tokens change the most on average.

For example, If we take the C++ and Python dataset, after interventions, we find tokens that are promoted the most for that particular intervening dataset for each layer. Averaging over all layers we get a set of ranked tokens that show highest promotion. These form our Characteristic token set. 
These token sets are stored in `token_sets/` directory. 

### 2. All Model Causal Intervention
The notebook `02_all_model_causal.ipynb` contains code to run and do causal analysis on 4 models, 
Gemma 4B, Gemma 1B, Llama 3B, Llama 1B. It is advisable to set the `DTYPE` to torch.float32 or torch.bfloat16 for best performance. 
The prompts are taken from `prompt_set/` directory and the characteristic token set from the previously generated `token_sets/` directory. Fisher score is present in `scores/` directory. 

Output of this notebook is stored in `full_compute/` as json files for each model. 

### 3. Graph Generation 
The notebook `03_graph_generator.ipynb` processes output from `full_compute/` to generate required graphs in the `graphs/` directory. 

### 4. Prompt Visualization
To visualize the outputs of different models on the prompt set, you can play with this notebook. 