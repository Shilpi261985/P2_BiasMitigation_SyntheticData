# BiasBios Synthetic Data Generation
### Submission Deadline: 31.7.2025
### Presentation: 8.8.2025
### Soft Deadline for Final Draft: 25.7.2025
## Outline for writing
### Materials and Methods
#### BiosBias Dataset
   - Description of the dataset (history and contents)
#### Model
   - Description of the chosen LLM and why. Include description of the machine GPU and CPU specs used for running the model.
#### Gender Classifier
   - Describe setup for classifier
   - Describe LIME explainer (and how it's used for identifying proxy words)
      - NOTE: The proxy word extraction probably works better if you FIRST remove names, pronouns, **stopwords**
   - You should do the classifier once without any masking and once masking names, pronouns, etc.
#### Synthetic Data Generation
Describe the process for generation (include the prompts you used). Note that you used only the accountant data and record the gender imbalance in the data.
   - Proxy words
      - Describe how you generated proxy word lists (lists should be provided in the appendix)
   - Job Ad
   - CV/Cover Letters
      - With explicit gender info
      - Without explicit gender info
      - Masking names and pronouns in bio before generation
        - With/without inclusion of words from proxy word lists
      - (Optional) Eliminating top proxy words from classifier + LIME experiments
#### Evaluation Experiments
- Repeat gender classification on CVs and Cover letters
   - Once for each: with gender, without gender, with masking
- Qualitative evaluation
   - Describe what you looked for when qualitatively evaluating the generated content
- You should do this for each of your generated datasets (baseline: gender given during generation, masked: as much gender info as possible masked, tone (optional): male assertive, female communal, proxies)
- Shortlisting (optional)
   - Use the same LLM (+ChatGPT for comparision, if time)
   - Provide 100 candidate CVs/cover letters along with the job ad, ask for shortlist of 10 best candidates
     - Do this once for CVs generated using the full bios, once for CVs generated using the masked content, once CVs using masked bios + proxy words
  - Compute gender ratios of top 10 each time. Even better, if time, run multiples and take averages
  - If time, do that same, but ask the model to explain it's reasoning before shortlisting
---
### Results
#### Dataset Analysis
Describe the results of your analysis on the BiosBias dataset.

#### Gender classifier
- Report accuracy, balanced accuracy, f1
- Qualitative analysis of high confidence and low confidence examples
   - See these notebooks:
      - https://colab.research.google.com/drive/1pi67-m54-BPOxEVwapM77dNNpFtsXtLZ,
      - https://colab.research.google.com/drive/1e0XVLn0Ov2BCVUS8bG3f3uq4otdN5Jkf?usp=sharing#scrollTo=6CR0CHHlwZTj
- Discussion of LIME explainer results

#### Evaluation Experiments
- Gender classification II
   - Do the same as before, but on the generated data (Train a new classifier on generated data WITHOUT including the BIOS)
- Qualitative evaluation
  - Describe your findings in terms of consistency of information, potential sources of bias in the generated CVs/Letters (e.g. your observation about the years as a proxy for age) and any other important observations.
  - Provide several illustrative examples from the generated data

<!-- ## Rough Project Timeline -->

## Repository Information
### Directories
- prompts:
    - prompt_template_jobAD.txt : for prompt used to generate jobADs
    - prompt_CV.txt : for prompt used to generate CV
    - prompt_CoverLetter : for prompt used to generate CoverLetter
- generated_txts:
    - generated_outputs.txt : for saving all generated jobADs (accountant)
    - generated_jobADs : folder for saving generated jobADs (accountant) seperately for 10 bios
    - CVs_CoverLetter_Accountant : folder for saving generated CVs and CoverLetters (accountant) separately for 10 bios
    - proxy_words.txt : generated proxy words, phrases that can show a persons (gender, race, ethinicity or nationality)
- csvs:
     - Bios_samples : folder for saving csvs for sampled(10) bios for all professions
     - accountant_complete.csv
     - df_accountant_lower.csv
- doc:
    - Doc_P2.docx : first draft of Project document
    - Doc_P2_5_6_25.docx : second draft of P2
      
### Notebooks
- load_Dataset.ipynb : has loaded main dataset and extracted sample Bios for each profession
- info_record.ipynb : has all the information and visualisation around dataset.
- model.ipynb : has uploaded model (Llama-2-7b-chat-hf) on GPU
- generate_jobAD.ipynb: for generating jobAds as per prompt text file for 10 sampled bios.
- generate_CV_CoverLetter.ipynb: to generate and save CV and Cover letter in separate text files.
- GenderClassification.ipynb: to explore gender classification using LIME text explainer (without masking)
- Classifier_with_lowercase_text : to explore gender classification using LIME but with lowercase texts(without masking)
- df_accountant_lower.ipynb : for df_accountant_complete in lower case
- masked_pronouns_genderClassification.ipynb : classification on masked pronouns

##
## Important Notes
<!-- **Next Meeting:** 13.5.2025, 15h, virtual -->
##
### Sensitive attributes
- gender: male, female
- race/nationality/ethnicity: black, hispanic, middle eastern, asian
- age: 20-30,30-40,40-50,50+
- religion: 
- *disability: physical, mental*
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
### Tasks
- Forward me info about timeline and requirements for writeup.
- Finalize the job ad.
<!-- - For now, stick to a single profession (accountant). -->
- CV\Cover letter generation
  - No names or contact information.
  <!-- - Instructions to make it easy to extract only the relevant text from the response. -->
  - Make sure any invented details are consistent with the bio, use real place names (companies/universities) as much as possible.
  - **Add option to include/exclude gender information (including proxy words) before generation**
- Identify obvious gender words in original dataset and save (identified as male or female)
    - gender pronouns (he\him\his, she\her\hers, they\them\theirs)
    - Names (probably use a "names" or "proper nouns" NLP library, e.g., spacy)
    - husband, father etc. (probably you can generate or find online)
- Generate preliminary proxy word lists for gender using classifier.
    <!-- - From dataset: https://colab.research.google.com/drive/1e0XVLn0Ov2BCVUS8bG3f3uq4otdN5Jkf?usp=sharing (similar to this notebook, but with gender classification) -->
    - Try also after removing gender pronouns and names.
    - Also, try on the generated CVs/Cover letters.
    - (OPTIONAL) Try on job ad (classifier trained on, e.g., bios)
- Generate preliminary proxy word lists using genAI
    - pronouns
    - social/familial/workplace roles
    - personality traits
    - e.g. 'Generate 10 words or phrases related to social roles that may appear in bios, CVs, or cover letters for accountants that could be proxies for gender.'
- Read generated CVs, cover letters, and job ads for existing 10 samples
    - Check for consistency, notes anything that doesn't look right.
- Compare old model to "meta-llama/Llama-3.2-3B-Instruct"
<!-- - Add variable to specify job ad generation type (use_candidate_info)
    - For 'use_candidate_info' the job ad should be created for the provided pool of 10/100 candidates. -->
<!-- - Add ability to specify degree level and retrieve corresponding samples from bios.
            
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
                return extracted_bios_samples -->

<!---    - **Add option to specifiy other sensitive attributes**  -->
<!-- - Add option to include proxy words
    <!-- - Add option to specify gender (combined with masking pronouns), this should also be an option for job ad creation
    <!-- - Add option to specifiy other sensitive attributes -->

<!-- generate_CV_CoverLetter(profession, bio, gender = False, other_attributes = None, proxy_words = None):
                '''
                If gender == false, then mask gender pronouns and do not specify gender label.

                other_attributes is a dictionary with keys "attribute name" and value "attribute" 
                    e.g., other_attributes = {'race' : 'black', 'sexual_orientation': 'straight'}

                proxy_words: list of proxy words for specified sensitive attributes.
                '''
                ...
                return generated_text -->
<!-- - Make sure files are saved as augmented csvs in a nice way (see below) -->

<!-- ### Detailed tasklist  -->
<!-- - **Prelimnary proxy wordlists**
    - Generate a list of 10 proxy words (or sentences) likely to appear in a CV or cover letter for a position as a [Profession] that would implicitly indicate that the applicant is [GENDER/RACE/NATIONALITY].  -->

<!-- - **Read generated 10 CVs, cover letters, and job ads for existing 10 accountant samples**
    - Check for consistency/quality
    - Compare Llama-3.2-3B-Instruct (especially if there are many consistency issues) -->
<!-- 
- Add ability to mask gender pronouns in bios (if we don't want to include gender information to generate letters, we want to mask this info)   -->
<!-- - Job-ad generation:
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
        - **Other job requirements (education level etc.)** -->
<!-- 
    <!-- - Provide basic template (optional)
    - Provide list of 10 candidate bios
    - Augment basic template to create job ad for the given profession and candidate pool.
    - End prompt with "Generated job ad:"
    - Only take text after "Generated job ad:" as response (so that you don't reprint the model input in your output).
    - (Optional) Experiment with different levels of seniority/desired candidates attributes in general. --> -->


 <!-- - It would be best to include an option for whether or not the gender is used in generating the application.
    - Include ability to specify race/nationality/ethnicity.
    - Include words/sentences that are "proxies" for e.g. gender/race. ("My main hobby is knitting vs. My main hobby is football.") -->
<!---- **Expand generation into a framework generating job applications for multiple samples and saving in CSV file.**
    - Should save as augmented subset of BiasBios dataset with job_ad_id in filename and extra columns for the CV and Cover letter
        - e.g., 'generated_txts/accountant/job_ad_id/100_random_no_gender.csv' containing 10 accountant samples augmented with CV and cover letter
        - And job ad could be saved to 'generated_txts/job_ad_id/job_ad.txt' along with the corresponding prompt 'generated_txts/job_ad_id/prompt.txt' -->
<!-- - Compare available models on HF in terms of pros and cons for our task.
    - meta-llama/Llama-3.2-1B-Instruct
    - meta-llama/Llama-3.2-3B-Instruct -->

<!-- - Organize csv folder into subfolders. -->
<!--- Further information on the dataset:
    - Are the gender distributions realistic?
    - Why are professors so overrepresented?
    - Does the distribution of samples per job reflect the real-world distribution?
    - Why these jobs? Just by frequency? (Note: all high-skilled, no blue collar)

- Create easy webUI for experimentation -->
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


#### 01 May 2025
- loaded proxy_words.txt file for proxy words and phrases to be used to check biases, in generated text folder.
- while checking quality and discrepancies with model **'Llama-2-7b'** in generated texts, its found:
  - Cover Letters: in many cover letters 'names' didnot appear, even when they were given in Bios.
  - CVs: generation of many CVs halted apruptly. At one place, even the sentence from Bio was genertaed as a third person.
  - Job Ads: mostly all generations halted incomplete.
- issue of incompleteness in text generation is solved by changing max_length of new tokens to 2048 (earlier 512). Job ADs, CVs and cover Letters are generated in complete length. (updated folder 'generated_txts')

#### 8 May 2025
- updated folders of generated texts
- generated new job ADs with model Llama3.2
- Model2 proved to be taking longer time to generate texts. Quality is a bit better.

#### 13 May 2025
- uploaded first draft of project document
- uploaded summarized job AD using model Llama3.2 in generated_txts folder

#### 5 June 2025
- uploaded second draft of P2 in doc folder
- uploaded GenderClassification.ipynb (without masking) and Classifier_with_lowercase_text.ipynb in src folder

#### 18 June 2025
- accountant_complete.csv
- df_accountant_lower.csv
- df_accountant_lower.ipynb : for df_accountant_complete in lower case
- masked_pronouns_genderClassification.ipynb : classification on masked pronouns
