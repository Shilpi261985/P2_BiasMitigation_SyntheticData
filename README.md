## BiasBios Synthetic Data Generation
#### 11 March 2025

File load_dataset.ipynb : 
- Loads the BiasBios Dataset from  https://huggingface.co/datasets/LabHC/bias_in_bios 
- As the data is already split in train, test and dev, we need to concatenate the data to get one whole dataframe. 
- Mapping of the occupation with the 'profession' column as described in Bias_in_Bios Dataset documentation, also mapping of gender column with 'Male' and 'Female' 
- No of samples (10) are extracted as per each profession and saved in separate CSV files. 

##
**Next Meeting:** 25.3.2025, 15h, in-person

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
- Create a prompt for generating a job ad for a given profession (profession should be a variable).
- Generate a CV and cover letter based on sample from the dataset and generated job ad.
    - It would be best to include an option for whether or not the gender is used in generating the application.
- Expand generation into a framework generating job applications for multiple samples and saving in CSV file.
- (Optional) compare available models on HF in terms of pros and cons for our task.

##
#### 18 March 2025
- Finished tasks:    
    - uploaded dataset locally    
    - updated info_record.ipynb with all information and visulaisation about dataset    
    - updated prompt_job_ad.ipynb with prompt for job ad.    
    - saved text files with prompt under 'prompts' folder.
    - Uploaded model Meta-Llama on GPU server
    - generated jobad file for one profession
    - generated CV and cover letter
    - (both have some issues, need to be discussed)
