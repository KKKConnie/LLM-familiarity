# LLM-Familiarity
## Overview
This repository provides a large-scale familiarity database for 27,624 Simplified Chinese lexical items, estimated with large language models (LLMs), including GPT-4o and Qwen-max. Beyond releasing the familiarity estimates themselves, the repository is designed to support their transparent use, reproducibility, and future extension. It documents the model settings and workflow used in the current study, provides guidance for adapting the framework to new variables, languages, and models, and includes step-by-step tutorials for practical research tasks.

## Contents
- [How this resource can support research](#how-this-resource-can-support-research)
- [Data and repository contents](#data-and-repository-contents)
  - [Familiarity datasets](#familiarity-datasets)
  - [Supporting materials](#supporting-materials)
- [Reproducibility, model currency, and versioning](#reproducibility-model-currency-and-versioning)
  - [Model settings](#model-settings)
  - [Code pipeline](#code-pipeline)
- [Extending the approach to new variables, languages, and models](#extending-the-approach-to-new-variables-languages-and-models)
  - [Suitability criteria](#suitability-criteria)
  - [Prompt engineering recommendations](#prompt-engineering-recommendations)
  - [Iterative calibration protocol](#iterative-calibration-protocol)
- [Step-by-step tutorials](#step-by-step-tutorials)
  - [Tutorial 1. Fine-grained data retrieval for stimulus selection](#tutorial-1-fine-grained-data-retrieval-for-stimulus-selection)
  - [Tutorial 2. Using LLM-derived familiarity to model lexical decision latencies](#tutorial-2-using-llm-derived-familiarity-to-model-lexical-decision-latencies)

## How this resource can support research

This resource is intended to support research in several complementary ways. 

Empirically, the released familiarity estimates can be used for stimulus selection, lexical control, and analyses of lexical processing; in our validation analyses, they also showed strong predictive validity for reaction times relative to the existing resources evaluated in the current study. 

Methodologically, the repository documents a scalable LLM-based workflow that can complement traditional human norming and extend familiarity estimation to larger vocabularies. 

More broadly, the framework may also support cross-linguistic work by providing a familiarity resource for Simplified Chinese that can be compared with normative datasets developed for alphabetic languages.

## Data and repository contents

### Familiarity datasets
All released familiarity datasets are organized in the `Data/2 norms` directory. These files contain the main familiarity estimates reported in the current study.

- **GPT-4o-derived datasets**
  - `norms_gpt4o_character_prompt.xlsx` (generated with the character prompt)
  - `norms_gpt4o_word_prompt.xlsx` (generated with the word prompt)
  - `norms_gpt4o_expression_prompt.xlsx` (generated with the expression prompt)

- **Qwen-max-derived dataset**
  - `norms_qwen_max.xlsx`

### Supporting materials
The repository also includes the key materials required to interpret and reuse the released datasets.

- **Target stimuli**: The complete list of 27,624 lexical items is available in `Data/0 wordlists/target_words.txt`.
- **Prompt template**: The exact prompt template used for data generation is available in `Data/1 prompts/prompt_template.txt`.
- **Variable descriptions**: Detailed definitions of all metrics and columns are provided in `Data/Variable Descriptions.xlsx`.

## Reproducibility, model currency, and versioning

To support reproducibility and future updates, the repository documents the code, model settings, and core parameter configurations needed to regenerate familiarity ratings and to examine representative validation analyses as models evolve.

> Note: Before running the generation pipeline, we recommend checking the latest official API documentation for interface changes, supported parameters, and log-probability options.

### Model settings

| Model | Version | Key parameters | Estimation strategy |
|---|---|---|---|
| GPT-4o | `gpt-4o-2024-08-06` | `temperature=0`, `logprobs=True`, `top_logprobs=7` | Single API call with log-probability-based estimation |
| Qwen-max | `qwen-max` | `temperature=0.7` | Mean of 30 independent iterations |

### Code pipeline

- **Generation**: `Code/01_generate_ratings.ipynb`  
  Generates familiarity ratings through API-based inference. To evaluate newer model versions or alternative parameter settings, users can update the model name and the relevant API parameter dictionary in this notebook and rerun the generation workflow on the same target word list.

- **Analysis**: `Code/02_data_analysis.ipynb`  
  Contains representative validation and downstream analysis examples used in the current study, including alignment with human familiarity norms and predictive modeling of lexical decision latencies.

#### Refreshing and evaluating updated outputs

To refresh the familiarity norms for a newer model version, users can update the model name and core parameter settings in `Code/01_generate_ratings.ipynb` and rerun the generation notebook on the same target word list. The resulting outputs can then be examined with `Code/02_data_analysis.ipynb`. 

#### External resources for validation
Some datasets used in the validation analyses are publicly available from their original sources but are not redistributed in this repository. Users who wish to rerun those analyses should obtain the relevant datasets separately. Detailed guidance on representative use cases is provided in the tutorials.

## Extending the approach to new variables, languages, and models

To facilitate extension beyond the current release, the repository also provides general guidance for adapting the framework to new psycholinguistic variables, languages, and LLMs.

### Suitability criteria
We suggest that a variable is well suited for LLM-based estimation when three conditions are met:  
(1) it has a clear operational definition;  
(2) human norms are available for validation; and  
(3) the target language is sufficiently represented in the model’s training corpora.  

These criteria are intended to help researchers evaluate whether a given construct can be estimated meaningfully and validated reliably within an LLM-based framework.

### Prompt engineering recommendations
Based on our implementation experience, several prompt-design principles appear particularly useful when adapting the framework.

- **Role specification**: Explicitly define the linguistic background or role of the model at the start of the prompt (e.g., as a native speaker of the target language). This helps anchor the intended judgment perspective.
- **Construct definition**: Provide a clear, rigorous definition of the target variable, together with an explicit description of the rating scale (e.g., "1 to 7, where 1 represents the minimum...").
- **Target identification**: Clearly indicate the item to be rated and, when relevant, explicitly reinforce the target language context (e.g., “Chinese word” rather than a generic “word”).
- **Output constraints**: Restrict the output format as much as possible, such as requiring a numerical response on a fixed scale. This reduces malformed outputs and facilitates downstream cleaning.
- **Typographic emphasis**: When critical instructions are easy to overlook, visual emphasis (e.g., CAPITALIZATION or other typographic highlighting) may help make key constraints more salient.
- **Language alignment**: Prompt language itself may influence model behavior. In practice, performance may vary depending on how the prompt language interacts with the model’s training data, so this factor should be evaluated empirically during calibration.


### Iterative calibration protocol
Before full-scale data generation, we recommend establishing a stable prompt-and-parameter configuration through an iterative calibration procedure based on a representative subset of stimuli.

- **Subset selection**: Begin with a representative sample of the target vocabulary rather than the full dataset. The subset should cover the major item types relevant to the intended application. 
- **Small-scale generation**: Run initial rating generation on this subset using candidate prompts and parameter settings.
- **Output review and cleaning**: Inspect the outputs carefully, even when strict format constraints are used, and identify potential non-numeric responses, malformed outputs, or other irregularities.
- **Prompt and parameter refinement**: Revise the prompt wording, output instructions, and key settings in light of the initial outputs.
- **Validation**: Evaluate the calibrated outputs against available human norms to assess alignment and overall validity. When relevant, also examine whether the resulting ratings show useful explanatory power for downstream behavioral measures, such as lexical processing performance.

## Step-by-step tutorials
> Note: The tutorial notebooks in this repository are intended for local execution after the repository has been downloaded. 

### Tutorial 1. Fine-grained data retrieval for stimulus selection

This tutorial demonstrates how to retrieve a targeted subset of lexical items from the familiarity datasets for stimulus design. The example below uses the GPT-4o word-level dataset to extract the top 10% most familiar two-character items.

#### Working path
- Tutorial notebook: `Tutorials/01_stimulus_selection.ipynb` (for local execution)
- Input dataset: `Data/2 norms/norms_gpt4o_word_prompt.xlsx`
- Output directory: `Tutorials/output/`

#### Input data structure
The input table should contain at least the following columns:
- `WORD`: the lexical item
- `Length`: the number of characters in the item
- `GPT_FAM_probs`: the GPT-4o familiarity estimate

Detailed definitions of all variables are provided in `Data/Variable Descriptions.xlsx`.

#### Procedure
1. Load the released familiarity dataset.
2. Restrict the data to two-character items (`Length == 2`).
3. Sort items by `GPT_FAM_probs` in descending order.
4. Select the top 10% highest-scoring items.
5. Export the resulting subset for later use in stimulus design.

#### Output
The tutorial exports a filtered item list, for example:
`Tutorials/output/gpt4o_top10pct_two_character_words.xlsx`

#### Notes
- The same workflow can be applied to other datasets by changing the input file and the familiarity column of interest.
- For the Qwen-max dataset, replace `GPT_FAM_probs` with `qwen_FAM_mean_30`.
### Tutorial 2. Using LLM-derived familiarity to model lexical decision latencies

## Citation

## Contact
Please address questions and suggestions to:
* DING Ziyi | 丁子益 | ziyi.ecnu@gmail.com | ZiyiDing7@github
* QIN Kangning | 秦康宁 | conniekk729@gmail.com | KKKConnie@github
