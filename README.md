# 🧠 LLM-familiarity
This repository contains the data and code associated with the manuscript.

## Repository Structure

### Code  

The **Code** folder provides scripts for generating familiarity ratings and performing data analyses. 

**✅ Ratings Generation & Data Analysis.py** 
 
| ✨ Section | 🔍 Details |
|------------|----------|
| **Familiarity Rating Generation** | GPT-4o<br>Qwen |
| **Descriptive statistics** | basic statistical index<br>t-test |
| **Correlation** | Pearson correlation by word length<br>partial correlation controlling for length |
| **Regression** | Univariate Linear Regression<br>Univariate Nonlinear Regression<br>Hierarchical Regression | 

### Data

The **Data** folder contains all datasets used in the analyses. 

| 🗂️ File Name | 📝 Description |
|------------|-------------|
| **27624_character_7_cleaned.xlsx** | Cleaned dataset for **character prompts**, used for *t-tests* comparing the effects of different prompts. |
| **27624_expression_7_cleaned.xlsx** | Cleaned dataset for **expression prompts**, used for *t-tests* comparing prompt effects, *correlation analyses* at the single-character level, and *regression analyses* (Naming task). |
| **27624_expression_7_cleaned_filtered.xlsx** | Filtered version of the expression dataset, retaining trials with **ACC > 85% (LDT task)**, used for *single-character regression analyses*. |
| **27624_unique_words.txt** | List of all stimulus words used in the experiments. |
| **27624_word_7_cleaned.xlsx** | Cleaned dataset for **word prompts**, used for *t-tests* comparing prompt effects, *correlation analyses*, and *regression analyses* for multi-character words (Naming task; from Hendrix et al., 2020). |
| **27624_word_7_cleaned_filtered.xlsx** | Filtered version of the word dataset, retaining trials with **ACC > 85% (LDT task)**, used for *multi-character regression analyses*. |
| **27624_word_7_cleaned_filtered_nam.xlsx** | Filtered version of the word dataset, retaining trials with **ACC > 85% (Naming task)**, used for *multi-character regression analyses* (from Zhang et al., 2023). |
| **Variable Descriptions.xlsx** | Description of variables, including detailed explanations for each column in the datasets. |

---

### 🚀 To be continued...
This repository is still being updated — more analyses and results will be added soon. 🌱
