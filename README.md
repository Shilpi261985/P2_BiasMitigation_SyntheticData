# BiasBios Synthetic Data Generation

File load_dataset.ipynb : 
--Loads the BiasBios Dataset from  https://huggingface.co/datasets/LabHC/bias_in_bios 
--As the data is already split in train, test and dev, we need to concatenate the data to get one whole dataframe. 
--Mapping of the occupation with the 'profession' column as described in Bias_in_Bios Dataset documentation, also mapping of gender column with 'Male' and 'Female' 
--No of samples (10) are extracted as per each profession and saved in separate CSV files. 

## Tasks
- Download model to GPU server
- Generate text based on prompt saved in seperate txt file
