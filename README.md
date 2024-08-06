# Integration of Imaging Features and Clinical Features for Early Detection of Lung Cancer


This project includes two files: 'Sybil_Project.ipynb' and 'Sybil ML Training.ipynb.' Sybil_Project provides functions to extract metadata from dicom files, prepare data for use in Sybil, run Sybil on data, and to use Sybil to perform image feature extraction. Sybil ML Training provides functions to pre-process data for use in machine learning models and functions to compare performance between models.

## Sybil_Project
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

