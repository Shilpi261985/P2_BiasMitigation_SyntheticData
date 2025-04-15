# BiasBios Synthetic Data Generation

## Repository Information
### Directories
- prompts:
    - prompt_template_jobAD.txt : for prompt used to generate jobADs
    - prompt_CV.txt : for prompt used to generate CV
    - prompt_CoverLetter : for prompt used to generate CoverLetter
- generated_txts:
    - generated_outputs.txt : for saving all generated jobADs (accountant)
    - generated_jobADs : folder for saving genertaed jobADs (accountant) seperately for 10 bios
    - CVs_CoverLetter_Accountant : folder for saving generated CVs and CoverLetters (accountant) separately for 10 bios
- csvs:
     - Bios_samples : folder for saving csvs for sampled(10) bios for all professions

### Notebooks
- load_Dataset.ipynb : has loaded main dataset and extracted sample Bios for each profession
- info_record.ipynb : has all the information and visualisation around dataset.
- model.ipynb : has uploaded model (Llama-2-7b-chat-hf) on GPU
- generate_jobAD.ipynb: for generating jobAds as per prompt text file for 10 sampled bios.
- generate_CV_CoverLetter.ipynb: to generate and save CV and Cover letter in separate text files.
##
## Important Notes
**Next Meeting:** 15.4.2025, 16h, online
##
## Tasks
<!-- ~~- Download model to GPU server~~

~~- Generate text based on prompt saved in seperate txt file~~

~~- Record information about the dataset in the Readme file:
    - Gender distribution overall
    - Gender distributaion per profession
    - Number of samples per profession
    - List of professions (and how they were chosen)
    - A couple text samples
    - How it was collected
    - Who is the sample population~~

~~- In Readme, describe contents of each (important) notebook.~~ -->
### Summary of main upcoming tasks
- For now, stick to a single profession.
- Add ability to mask gender pronouns from bios.
- Fix truncation with either "max_length" and/or stop token condition.
- Generate preliminary proxy word lists for gender and choice of race/ethnicity/nationality.
- Read generated CVs, cover letters, and job ads for existing 10 samples
    - Check for consistency, notes anything that doesn't look right.
    - If there are inconsistencies try:
        - Generating CV and cover letter simultaneously
        - Or using CV as extra input for cover letter
        - Or use "meta-llama/Llama-3.2-3B-Instruct"
- Add variable to specify job ad generation type (use_candidate_info)
    - For 'bios' the job ad should be created for the provided pool of 10/100 candidates.
- Add ability to specify degree level and retrieve corresponding samples from bios.
            
            generate_job_ad(profession, gender = False, other_requirements = None, use_candidate_info = False, candidate_bios):
                '''
                If gender == false, then mask gender pronouns and do not specify gender label.
                
                other_requirements is a dictionary with keys "requirement type" and value "requirement" 
                    e.g., other_attributes = {'education' : 'master', 'bio_contains': [activist, senior]}
                
                If use_candidate_info == False, don't use any candidate info to generate job ad.

                candidate_bios: selected bios used for generation.
                '''
                ...
                return generated_text

            create_candidate_pool(profession, pool_type = 'random', 'gender_parity' or 'keyword', keywords = None):
                '''
                Function for creating desired pool of applicants for job ad generation.
                '''
                return extracted_bios_samples
- For CV/cover letters
    - Add option to specify gender (combined with masking pronouns), this should also be an option for job ad creation
    - Add option to specifiy other sensitive attributes

            generate_CV_CoverLetter(profession, bio, gender = False, other_attributes = None, proxy_words = None):
                '''
                If gender == false, then mask gender pronouns and do not specify gender label.

                other_attributes is a dictionary with keys "attribute name" and value "attribute" 
                    e.g., other_attributes = {'race' : 'black', 'sexual_orientation': 'straight'}

                proxy_words: list of proxy words for specified sensitive attributes.
                '''
                ...
                return generated_text
- Make sure files are saved as augmented csvs in a nice way (see below)

### Detailed tasklist 
- **Prelimnary proxy wordlists**
    - Generate a list of 10 proxy words (or sentences) likely to appear in a CV or cover letter for a position as a [Profession] that would implicitly indicate that the applicant is [GENDER/RACE/NATIONALITY]. 

- **Read generated 10 CVs, cover letters, and job ads for existing 10 accountant samples**
    - Check for consistency/quality
    - Compare Llama-3.2-3B-Instruct (especially if there are many consistency issues)

- Add ability to mask gender pronouns in bios (if we don't want to include gender information to generate letters, we want to mask this info)  
- Job-ad generation:
    - VARIANTS:
        - Basic template (no info besides profession)
        - DONE: Bespoke job ad (written for a specific candidate)
        - **Using a pool of 10 or 100 samples from dataset** (writing a job ad for which they would be an expected applicant pool)
            - Random Sampling
            - Sampling with specified gender distribution (e.g. 50/50)
            - **Keyword/Specialized retrieval** (e.g., search for "bachelor", "masters" , "experienced" or semantic similarity)
    - OPTIONAL INPUT INFORMATION:
        - Gender
        - Other sensitive attributes
        - Instruction to write/adapt for specific demographic group
        - **Other job requirements (education level etc.)**

    <!-- - Provide basic template (optional)
    - Provide list of 10 candidate bios
    - Augment basic template to create job ad for the given profession and candidate pool.
    - End prompt with "Generated job ad:"
    - Only take text after "Generated job ad:" as response (so that you don't reprint the model input in your output).
    - (Optional) Experiment with different levels of seniority/desired candidates attributes in general. -->
- CV and cover letter generation
    - **Add option to specify gender (combined with masking pronouns)**
    - **Add option to specifiy other sensitive attributes**
    - Add option to include proxy words
    - Generate CV and cover letter together (if there are consistency issues)
    <!-- - It would be best to include an option for whether or not the gender is used in generating the application.
    - Include ability to specify race/nationality/ethnicity.
    - Include words/sentences that are "proxies" for e.g. gender/race. ("My main hobby is knitting vs. My main hobby is football.") -->
- **Expand generation into a framework generating job applications for multiple samples and saving in CSV file.**
    - Should save as augmented subset of BiasBios dataset with job_ad_id in filename and extra columns for the CV and Cover letter
        - e.g., 'generated_txts/accountant/job_ad_id/100_random_no_gender.csv' containing 10 accountant samples augmented with CV and cover letter
        - And job ad could be saved to 'generated_txts/job_ad_id/job_ad.txt' along with the corresponding prompt 'generated_txts/job_ad_id/prompt.txt'
<!-- - Compare available models on HF in terms of pros and cons for our task.
    - meta-llama/Llama-3.2-1B-Instruct
    - meta-llama/Llama-3.2-3B-Instruct -->

<!-- - Organize csv folder into subfolders. -->
- Further information on the dataset:
    - Are the gender distributions realistic?
    - Why are professors so overrepresented?
    - Does the distribution of samples per job reflect the real-world distribution?
    - Why these jobs? Just by frequency? (Note: all high-skilled, no blue collar)

- Create easy webUI for experimentation
##

## Progress Reports
#### 11 March 2025

File load_dataset.ipynb : 
- Loads the BiasBios Dataset from  https://huggingface.co/datasets/LabHC/bias_in_bios 
- As the data is already split in train, test and dev, we need to concatenate the data to get one whole dataframe. 
- Mapping of the occupation with the 'profession' column as described in Bias_in_Bios Dataset documentation, also mapping of gender column with 'Male' and 'Female' 
- No of samples (10) are extracted as per each profession and saved in separate CSV files. 
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

#### 13 April 2025
- load_Dataset.ipynb : has loaded main dataset and extracted sample Bios for each profession
- info_record.ipynb : has all the information and visualisation around dataset.
- model.ipynb : has uploaded model (Llama-2-7b-chat-hf) on GPU
- generate_jobAD.ipynb : for generating jobAds as per prompt text file for 10 sampled bios.
- prompt_template_jobAD.txt : file for prompt used to generate jobADs
- created new folder generated_txts to save file generated_outputs.txt for saving all generated jobADs
- generate_CV_CoverLetter.ipynb : file to generate and save CV and Coverletter in sepearte text files.
- prompt_CV.txt : file for prompt to generate CV
- prompt_CoverLetter.txt : file for prompt to generate Cover Letter
- saved genertaed CVs, CoverLetter and Job Ads for 'Accountant' under 'generated_txts' folder
