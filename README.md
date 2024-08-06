# Integration of Imaging Features and Clinical Features for Early Detection of Lung Cancer

Sybil is a deep learning model that uses a single low-dose chest computed tomography (LDCT) scan to predict the likelihood of lung cancer development 1-6 years after a screening. Although promising, Sybil and other imaging-based models often overlook valuable clinical information, which is essential for comprehensive evaluation. Therefore, this project develops machine learning algorithms to integrate CT imaging features and clinical features to provide a more accurate and holistic lung cancer risk assessment.  

This project includes two files: 'sybil_training.ipynb' and 'sybil_ml_training.ipynb.' sybil_training provides functions to extract metadata from dicom files, prepare data for use in Sybil, run Sybil on data, and to use Sybil to perform image feature extraction. sybil_ml_training provides functions to pre-process data for use in machine learning models and functions to compare performance between models.

## sybil_training
### Extracting Metadata from Dicom Files

In order to determine which sets of scans are suitable for training, this project includes functions to extract metadata from dicom files. The function 'get_first_file_in_every_folder' creates a list of directories for the first file in every terminal folder in a nested directory. Assuming scans are organised in a manner similar to the following:

```
  ├── <AccessionNumber>                   
  │   ├── <scan_id1>
  |   |  |── <dicom_file1>
  |   |  |── <...>
  │   ├── <scan_id2>   
  │   ├── <...>    
```

'get_first_file_in_every_folder' will return a list containing the directories for one dicom file for every scan. With this list of directories, the function 'make_dicom_metadata_df' will create a dataframe containing metadata from each dicom file.

### Determining Necessary Values for Sybil Training

The functions 'determine_diagnosis' and 'determine_diagnosis_year' will add columns to a dataframe representing whether a patient was diagnosed with lung cancer and the time until a positive diagnosis or time until last negative diagnosis, respectively.

### Running Sybil Evaluation

The function 'run_sybil_evatuation_on_dataframe' will run Sybil on every entry in a dataframe and return risk scores for every entry, the AUC, and the C-index. By default, Sybil uses an ensemble of 5 models. To run a particular Sybil model on a dataframe, use the function 'run_specific_sybil_eval_on_dataset.'

### Sybil Feature Extraction

The function 'extract_ct_image_feature' takes in a dataframe that includes a column named 'Directory' that specifies the directory to a set of dicom files and uses Sybil to perform imaging feature extraction on every entry in the dataframe.

## sybil_ml_training

### Exploratory Data Analysis

The function 'get_dataframe_null_metrics' creates a dataframe that lists the unique values,	number of unique values, and number of null values for every column of a dataframe.

### Calculating PLCO Scores

The functions 'calculate_plco_2012' and 'calculate_plco_2014' calculate the 2012 and 2014 PLCO scores, respectively.

### Machine Learning Training

The functions 'train_nlst_model' and 'evaluate_ucla_model' allow one to perform a a cross-validated grid search on a machine learning model on the NLST dataset and evaluate the best performing model on the UCLA dataset.

