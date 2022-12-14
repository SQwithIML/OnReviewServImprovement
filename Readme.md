# Determining Directions of Service Quality Management using Online Review Mining with Interpretable Machine Learning

## Explanation
- Under construction

## Implementation

- **Our Environment**
  - OS : Ubuntu 18.04 (we checked this code file works on Window OS)
  - python == 3.7  
  - conda >= 4.10  

Run this code to create your own virtual environment. (you can skip it, but we recommend creating a new virtual environment for this implementation)
```bash
conda create -n 'env_name' python=3.7 
```
Activate your environment
```bash
conda activate 'env_name'
# (or) source activate 'env_name'
```

Run this code to clone the files into your local environment.  
```bash
git clone https://github.com/SQwithIML/OnReviewServImprovement.git
```
Move to `OnReviewServImprovement` folder
```bash
cd OnReviewServImprovement/
```

Run the below code to install the required package for this implementation.  
```bash
#(if you need) pip install --upgrade pip
pip install -r requirements.txt
```

### Code structure
```bash
root
├─Params.yaml
├─identifyServiceFeatures.py
├─estimateImportance.py
├─src
│   ├─ __init__.py
│   ├─ main_components.py
│   ├─ preprocessors.py
│   └─ utils.py
├─Datasets
│   └─ Custom
│      └─***.** (filename.extension)
└─Results
    ├─ [1]LDA - Result_Folder_for_each_combination
    ├─ [2]ML - Hyper_parameter_tuning_Reports
    ├─ [3]IPA - Plot_for_Importance_Performance_Analysis
    └─ etc.
```
### Note
Before you run the below code, please check the `Params.yaml` file.
In `Params.yaml`, you can set the parameters for our framework and custom data path.
Since a grid search will be performed to find optimal LDA and ML models, you have to set the candidates of each hyperparameter of both models.
Also, you can change the name of `.yaml` file. If you change it, please enter the file name at `--ymal="ymal_name"` in the below codes.

Due to the copyright, we cannot provide the review data that we employed for our paper. Instead, we provide open-source review data for this implementation.
To implement this framework for your review datasets (star rating required), just modify `ModifiedCustomizedPreprocessor` in `identifyServiceFeatures.py` to fit your datasets, and change `USE_DATATYPE` to `"Custom"` and `CUSTDATA_PATH` in `Params.yaml` . For this, please refer to the example code in `ModifiedCustomizedPreprocessor`. 

### [1] Review data preprocessing and service feature identification
- Execution list
  * Text preprocessing
  * LDA Topic modeling

Running the code below generates preprocessed datasets in `/Results` folder and a `summary.txt` and `report.txt` with a words-topic list for each combination of candidates in each folder in `/Results/[1]LDA/`.  
```bash
python identifyServiceFeatures.py --yaml="Params"
```

Referring to the `summary.txt` and words-topic list in `report.txt`, choose the best results of LDA topic modeling and name each topic.
After that, Enter the folder name at `LDA_RESULT_IDX` and the name of each topic in `TopicList` in `yaml`file.

### [2~3] Global importance estimation using optimal prediction model
- Execution list
  * Preparing the datasets for training (creating review-feature matrix and spliting datasets)
  * K cross validation for hyper-parameter tuning and finding optimal prediction model
  * Estimation of global importance of service features
  * Importance Performance Analysis (plot)

Running the code below generates `report.txt` that records the performance of each model in `/[2]ML` folder and saves the plot for Importance Performance Analysis (IPA) in `/[3]IPA` folder.
```bash
python estimateImportance.py --yaml="Params"
```

