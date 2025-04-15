# BiasBios Synthetic Data Generation

## Repository Information
### Directories
-prompts:
-generated_txts:
-csvs:

### Notebooks
- load_Dataset.ipynb : has loaded main dataset and extracted sample Bios for each profession
- info_record.ipynb : has all the information and visualisation around dataset.
- model.ipynb : has uploaded model (Llama-2-7b-chat-hf) on GPU 

#### 11 March 2025

File load_dataset.ipynb : 
- Loads the BiasBios Dataset from  https://huggingface.co/datasets/LabHC/bias_in_bios 
- As the data is already split in train, test and dev, we need to concatenate the data to get one whole dataframe. 
- Mapping of the occupation with the 'profession' column as described in Bias_in_Bios Dataset documentation, also mapping of gender column with 'Male' and 'Female' 
- No of samples (10) are extracted as per each profession and saved in separate CSV files. 

##
**Next Meeting:** 15.4.2025, 16h, online

## Tasks
~~- Download model to GPU server~~

~~- Generate text based on prompt saved in seperate txt file~~

~~- Record information about the dataset in the Readme file:

    - Gender distribution overall
    - Gender distributaion per profession
    - Number of samples per profession
    - List of professions (and how they were chosen)
    - A couple text samples
    - How it was collected
    - Who is the sample population~~
- Create a (instruction-based) prompt for generating a job ad for a given profession (profession should be a variable).
    - Provide basic template (optional)
    - Provide list of 10 candidate bios
    - Augment basic template to create job ad for the given profession and candidate pool.
    - End prompt with "Generated job ad:"
    - Only take text after "Generated job ad:" as response (so that you don't reprint the model input in your output).
    - (Optional) Experiment with different levels of seniority/desired candidates attributes in general.
- Generate a CV and cover letter based on sample from the dataset and generated job ad.
    - It would be best to include an option for whether or not the gender is used in generating the application.
    - (Optional) Include ability to specify race/nationality/ethnicity.
    - (Optional) Include words/sentences that are "proxies" for e.g. gender/race. ("My main hobby is knitting vs. My main hobby is football.")
- Expand generation into a framework generating job applications for multiple samples and saving in CSV file.
- (Optional) compare available models on HF in terms of pros and cons for our task.
    - meta-llama/Llama-3.2-1B-Instruct
    - meta-llama/Llama-3.2-3B-Instruct
- In Readme, describe contents of each (important) notebook.
- Organize csv folder into subfolders.

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

##
#### 13 April 2025
- load_Dataset.ipynb : has loaded main dataset and extracted sample Bios for each profession
- info_record.ipynb : has all the information and visualisation around dataset.
- model.ipynb : has uploaded model (Llama-2-7b-chat-hf) on GPU
- Updated src folder with generate_jobAD.ipynb for generating jobAds as per prompt text file for 10 sampled bios.
- updated prompts folder with prompt_template_jobAD.txt file for prompt used to generate jobADs
- created new folder generated_txts to save file generated_outputs.txt for saving generated jobADs
- uploaded generate_CV_CoverLetter.ipynb file to generate and save CV and Coverletter in sepearte text files.
