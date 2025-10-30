# ML Pipeline with DVC

This repository contains a machine learning pipeline managed with DVC (Data Version Control). The pipeline consists of several stages from data ingestion to model evaluation.

## Pipeline Stages

### 1. Data Ingestion
This stage handles the initial data collection.
```bash
dvc repro data_ingestion
```
Dependencies:
- `src/data_ingestion.py`
Outputs:
- `data/raw/`

### 2. Data Preprocessing
This stage processes the raw data into a format suitable for feature engineering.
```bash
dvc repro data_preprocessing
```
Dependencies:
- `src/data_preprocessing.py`
- `data/raw/`
Outputs:
- `data/processed/`

### 3. Feature Engineering
This stage creates features from the processed data.
```bash
dvc repro feature_engineering
```
Dependencies:
- `src/feature_engineering.py`
- `data/processed/`
Outputs:
- `data/features/`

### 4. Model Building
This stage trains the machine learning model.
```bash
dvc repro model_building
```
Dependencies:
- `src/model_building.py`
- `data/features/`
Outputs:
- `model.pkl`

### 5. Model Evaluation
This stage evaluates the model's performance.
```bash
dvc repro model_evaluation
```
Dependencies:
- `src/model_building.py`
- `model.pkl`
Outputs:
- `metrics.json`

## Running the Complete Pipeline

To run the entire pipeline from start to finish:
```bash
dvc repro
```

## Checking Pipeline Status
To see the current status of the pipeline:
```bash
dvc status
```

## Viewing Metrics
To view the model's performance metrics:
```bash
dvc metrics show
```

## Adding New Stages to Pipeline

To add a new stage to the pipeline, use the `dvc stage add` command with the following parameters:
- `-n, --name`: Name of the stage
- `-d, --deps`: Dependencies (can be specified multiple times)
- `-o, --outs`: Outputs (can be specified multiple times)
- `-m, --metrics`: Metrics files to track
- `--plots`: Plots files to track
- `cmd`: The command to execute

Example:
```bash
dvc stage add -n model_eveluation -d .\src\model_building.py -d model.pkl --metrics metrics.json python .\src\model_evaluation.py 
```
## Pipeline Visualization
To visualize the pipeline structure:
```bash
dvc dag
```