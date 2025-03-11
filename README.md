# BiasBios Synthetic Data Generation

File load_dataset.ipynb : 
--Loads the BiasBios Dataset from  https://huggingface.co/datasets/LabHC/bias_in_bios 
--As the data is already split in train, test and dev, we need to concatenate the data to get one whole dataframe. 
--Mapping of the occupation with the 'profession' column as described in Bias_in_Bios Dataset documentation, also mapping of gender column with 'Male' and 'Female' 
--No of samples (10) are extracted as per each profession and saved in separate CSV files. 

## Tasks
- Download model to GPU server
- Generate text based on prompt saved in seperate txt file
- Record information about the dataset in the Readme file:
    - Gender distribution overall
    - Gender distributaion per profession
    - Number of samples per profession
    - List of professions (and how they were chosen)
    - A couple text samples
    - How it was collected
    - Who is the sample population

- Generate a CV based on sample from dataset (using the prompt saved in txt).
    - It would be best to include an option for whether or not the gender is used in generating the CV.
- Exand CV generation into a framework generating CVs for multiple samples and saving in CSV file.
- create a pandas dataframe with this sample + new column containing CV text.
- (Optional) compare available models on HF in terms of pros and cons for our task.
