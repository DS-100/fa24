---
layout: page
title: NLP Graduate Project
nav_exclude: true
description: Specifications for the NLPgrad project for Data 200.
markdown: kramdown
---

{: .warning }
⚠️ This content is archived as of March 2026 and is retained exclusively for reference. [Find current offerings.](https://ds100.org/)


# Graduate Project 2: Natural Language Processing
{:.no_toc}

* TOC
{:toc}

## Project Description: Natural Language Processing

A common task in real-life data analysis involves working with text data. In this project, we will work with a dataset consisting of natural language questions asked by humans and answers provided by chatbots.

### Project Goals
{:.no_toc}

- Gain practical experience with text data by applying techniques like embedding generation, tokenization, and topic modeling.
- Analyze a real-world dataset of chatbot conversations, including human questions, responses, and user votes.
- Formulate specific, data-driven questions and use the dataset to answer these questions with evidence.

### Dataset Description
{:.no_toc}

The source dataset link is [here](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations){:target="_blank"}. The author describes the dataset as follows:

> This dataset contains 33K cleaned conversations with pairwise human preferences. It is collected from 13K unique IP addresses on the Chatbot Arena from April to June 2023. Each sample includes a question ID, two model names, their full conversation text in OpenAI API JSON format, the user vote, the anonymized user ID, the detected language tag, the OpenAI moderation API tag, the additional toxic tag, and the timestamp.

#### Main Dataset

`chatbot-arena-conversations.jsonl.gz`: The primary dataset with over 25,000 cleaned chatbot conversations. It includes the question, responses from two chatbot models, user votes, and anonymized user information. It has gone through preprocessing to remove non-English conversations, multiple rounds of conversations, and toxic or harmful content.

#### Auxiliary Datasets

You are given the following two auxiliary datasets that you can use to help with your analysis:

**Embeddings**

  - `chatbot-arena-prompts-embeddings.npy`: Precomputed 256-dimensional embeddings for the human questions, useful for modeling and analysis.
  - `chatbot-arena-model_a_response-embeddings.npy`: Precomputed 256-dimensional embeddings for the model responses, useful for modeling and analysis.
  - `chatbot-arena-model_b_response-embeddings.npy`: Precomputed 256-dimensional embeddings for the model responses, useful for modeling and analysis.

**Topic Modeling and Hardness Score Data**

  - `chatbot-arena-gpt3-scores.jsonl.gz`: GPT-3.5-generated labels, including topic models and hardness scores for each question, providing additional features for analysis.
The detailed descriptions of each dataset can be found in the notebook below.


## Action Items

You are required to perform **(1) Exploratory Data Analysis (EDA)** and **(2) Modeling (Task A and Task B)** for this project.

### Exploratory Data Analysis

During EDA, you have to analyze the dataset to uncover patterns and insights. Formulate questions such as:

- What is the win rate of different models?
- What topics are most common?
- Do different judges have different preferences?
- What factors make a question hard?

You can get started with the following starter notebook for EDA: [`nlp-eda-starter.ipynb`](https://data100.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FDS-100%2Ffa24-student&urlpath=lab%2Ftree%2Ffa24-student%2Fgrad-proj%2Fnlp-chatbot-analysis%2Fnlp-eda-starter.ipynb&branch=main).

See below in the description for [Milestone 2](#milestone-2-eda) for detailed instructions for the report.

### Project Tasks

Now, we aim to better understand the different chatbot models! Please complete both Task A and B. We have included example questions to consider, but you are expected to come up with your own questions to answer.

For both tasks, you will be working with the training set provided. But you are also expected to perform prediction on a test set (`./test-set/arena-test-set-prompt-and-responses.jsonl.gz`). This data contains fields `question_id`, `prompt`, `model_a`, `model_b`, `model_a_response`, and `model_b_response`. **You are expected to predict the winner and the hardness score for tasks A and B respectively.** Feel free to also use existing or new feature-transformed data (e.g. embeddings etc.) to improve predictions. (For example, we have already provided the embedding data for you which is an example of feature-transformed data in the same directory if you end up needing this feature).

**You should submit your final prediction as a `csv` file with three columns `question_id`, `winner`, `hardness_score`. The `winner` column should be one of the four values: `model_a`, `model_b`, `tie`, or `tie (bothbad)`. The `hardness_score` should be an integer from 1 to 10.**


#### *Task A: Modeling the Winning Model*
{:.no_toc}
Predict which chatbot model will win the user vote based on the prompt and model responses.

Steps you can take:
1. Start by analyzing features such as the length, text characteristics, and embeddings of the prompt.
2. Compare the outputs of the two chatbot models to find patterns.
3. Use a classification model (e.g., logistic regression) to predict the winner given `prompt`, `model_a`, `model_b`, `model_a_response`, and `model_b_response`.
4. Use appropriate metrics to evaluate the performance of your model.

One hint would be to utilize topic modeling data by first clustering prompts given their embeddings, then for each cluster, train a model to predict the winner. Also, feel free to use the hardness score to help with the prediction.

#### *Task B: Hardness Prediction*
{:.no_toc}
Predict the difficulty of a question, ranging from 1 to 10, using the available features. For example, if a prompt’s score is 1, we expect the weak model to be able to answer the question. If the score is 10, we expect the question to be hard, maybe only GPT4 can answer it.

Steps you can take:
5. Start by examining the question embeddings and topic modeling data. Look for patterns that might help predict question difficulty.
6. Use linear regression to predict the hardness score. Incorporate relevant features from the data to improve your predictions.
7. Ensure that your model predicts integer values between 1 and 10.
8. Use appropriate metrics to evaluate the performance of your model.

One challenging aspect here is that the output score should be an integer value, while linear regression is used for continuous data.

Additionally, here are some example questions about the project that you are welcome to explore.
> Modeling: Perform some modeling tasks given our ground truth labels. Can you train a logistic regression model to predict the winner-given embeddings? How about a K-means clustering model to cluster the questions? Can you use linear regression to predict the hardness score? We expect you to demonstrate how the well model works and how to evaluate them. You should justify the choice of model and the evaluation metrics. You should also discuss the limitations of the model and how to improve them.

> Analysis: By leveraging the question embeddings, can we find similar questions? How repeated are the questions in the dataset? Can you reproduce the Elo score rating for the chatbots and come up with a better ranking? How can we make sense of the data overall?

Resources
- [Joey’s EDA and Elo rating modeling](https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH){:target="_blank"} is a great resource to get started with the EDA. Note that (1) the plot is made with Plotly, we recommend you to reproduce the plot with Matplotlib or Seaborn, and (2) the Elo rating is a good modeling task to reproduce but we expect you to do more than just that (for example, demonstrate how Elo rating works and how to calculate it in your report).

- [An intuitive introduction to text embeddings](https://stackoverflow.blog/2023/11/09/an-intuitive-introduction-to-text-embeddings/){:target="_blank"} is a good resource to understand what is text embeddings and how to use them.

- [Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system) and [Bradley-Terry model](https://en.wikipedia.org/wiki/Bradley%E2%80%93Terry_model){:target="_blank"} are essential to model a ranking among the pairwise comparison.
- [Huggingface pipeline](https://huggingface.co/docs/transformers/en/main_classes/pipelines){:target="_blank"} has many implementations of common NLP tasks for you to use, including sentiment analysis, summarization, text classification, etc.

- [spaCy](https://spacy.io/usage/spacy-101){:target="_blank"} is a wonderful library containing classifical NLP tasks like tokenization, lemmatization, etc.

## Milestone Descriptions

### Milestone 1: Group Formation + Research Proposal (5%) - October 14, 2024

The first deliverable of your group project is just to form your group, choose a dataset, and submit your implementation plan to [this Google form](https://forms.gle/5FHyda3m7J4Dbu58A){:target="_blank"} by **11:59 pm on October 14**. The implementation plan should consist of a series of steps for completing the project along with a timeline. You may form groups of 2 or 3 people with any Data 200/200A/200S student.

The rubric for this milestone is as follows:
- Short paragraph description of implementation plan and timeline (2%).
- Forming teams by the deadline (3%).

<a name = 'milestone-2-eda'></a>

### Milestone 2: EDA + Internal Peer Review (10%) - October 28, 2024

The milestone is intended to keep you on track to meet your project goals. You will need to submit an exploratory data analysis report to [this Gradescope assignment](https://www.gradescope.com/courses/827978/assignments/5159878){:target="_blank"} by **11:59 pm on October 28**. This will include submitting both a report of your results so far as well as all code necessary to replicate your results. Please answer all the questions below. Your submission should include:

- **Data Sampling and Collection**
  - How was the data read and sampled for your EDA process?
  - Was there any potential bias introduced in the sampling process?
- **Data Cleaning**
  - What type of data are you currently exploring?
  - What is the granularity of the data?
  - What does the distribution of the data look like? Are there any outliers? Are there any missing or invalid entries?
  - The data is not structured. How did you turn it into a structured format? What features have you engineered?
- **Exploratory Data Analysis**
  - Is there any correlation between the variables you are interested in exploring?
  - How would you cleanly and accurately visualize the relationship among variables?
  - What are your EDA questions? (For example, are there any relationships between A and B? What is the distribution of A?).
  - Do you need to perform data transformations?
- **Figures(tables, plots, etc.)**
  - Descriptions of your figures. Takeaways from the figures.
  - These figures must be of good quality (i.e. they must include axes, titles, labels, etc.) and they must be relevant to your proposed analysis.

Concretely, here are the minimal requirements for EDA for each project. Using your knowledge from Data 200, what would be appropriate data visualizations? You are welcome to do more than the minimal requirements.

  - Ranking of the model based on their win rate or ELO ratings.
  - Distribution of the prompt and response length.
  - Hardness score distribution and its correlation with the models (e.g. GPT4 wins on hardest prompts).
  - (Open-ended) Visualize the "variance" in model performance (see [LMSys Leaderboard](https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard){:target="_blank"} for an example).
  - (Open-ended) Explore the prompt topics in the dataset (topic modeling).

Every member of the group also needs to submit the internal peer review [Gradescope assignment](https://www.gradescope.com/courses/827978/assignments/5159798){:target="_blank"} for this checkpoint by **11:59 pm on October 28**. This form is intended to record your and your group members' progress in the project. The records will be confidential to the teaching staff and will not be shared with other students.

The rubric for this milestone is as follows:
- Data Sampling and Collection (0.5%).
- Data Cleaning (3%).
- Exploratory Data Analysis (3%).
- Figures (tables, plots, etc.) (3%).
- Internal Peer Review (0.5%).

### Milestone 3: Mandatory Check-In (7.5%) - November 8, 2024

The purpose of this milestone is to ensure you are making progress and on schedule to submit the first draft of the project in approximately two weeks time. You will be required to make a document summarizing your progress so far, including your EDA and modeling results. You are required to submit the report to [this Gradescope assignment](https://www.gradescope.com/courses/827978/assignments/5045723){:target="_blank"} by **11:59 pm on November 8**. The staff member will skim the report before the meeting and give you guidance on the project as a whole.

For the check-in we would like for you to prepare brief answers to the following questions about the modeling process:
- What model do you plan on using and why?
- Does your model require hyperparameter tuning? If so, how do you approach it?
- How do you engineer the features for your model? What are the rationales behind selecting these features?
- How do you perform cross validation on your model?
- What loss metrics are you using to evaluate your model?
- From a bias-variance tradeoff standpoint, how do you assess the performance of your model? How do you check if it is overfitting?
- How would you improve your model based on the outcome?
- Are there any further extensions to your model that would be worth exploring?

The rubric for this milestone is as follows:
- Exploratory Data Analysis (1.5%).
- Feature Engineering (2%).
- Modeling Approaches (3%).
- Preliminary Results (1%).

### Milestone 4: Internal Peer Review (2%) - November 22, 2024

The internal peer review is for checking if each member of the group is contributing to the project and how the tasks are distributed among members. This is graded on completion.  The internal peer review [Gradescope assignment](https://www.gradescope.com/courses/827978/assignments/5159827){:target="_blank"} for this milestone is due by **11:59 pm on November 22**.

### Milestone 5: Project Report First Draft (18%) - December 2, 2024

The first draft of your final report, please see below for more information on what you should aim to submit. You do not need to submit the video and test set performance components for milestone 5, but you are expected to submit a comprehensive written report that summarizes your analysis.

Please refer to the section on the [Final Project Report](#final-project-report) for more information on how your first draft will roughly be graded. Your first draft will be graded more leniently than your final submission, but we’re still looking for largely the same elements. You do not need to submit the video and test set performance components for milestone 5, but you are expected to submit a comprehensive written report that summarizes your analysis.

Submit to the [first draft project report assignment](https://www.gradescope.com/courses/827978/assignments/5045727/) on Gradescope by **11:59pm on December 2**.

### Milestone 6: External Peer Review (7.5%) - December 6, 2024

Each group will peer review a project from another group; each group will be graded together based on the feedback they provide in their review. Each review should include the following components:

1. (1.5%) A summary of the report. The summary should address at least the following:
- What is the conclusion drawn from the EDA and modeling results?
- What data modeling/inference techniques do the group primarily use to gain insights into their research question? Why are these techniques suitable for the task?
- What are the next steps a researcher can take if they want to improve their model further based on the work in the project?

2. (6%, 1% per component) An evaluation of the report based on the Data Science Lifecycle. The review should include at least **one strong point and one suggestion for improvement** for each of the following components in the project:
- Data collection and sampling
- Data cleaning
- Exploratory data analysis (data wrangling, visualization, etc.)
- Data modeling (feature engineering, selection of the model, and evaluation of the model's performance, etc.)
- Inference (do the results from the model sufficiently support the conclusion within the report?)
- Discussion (does the report effectively discuss the limitations of the methods used and the implications of the results?)

The external peer review is also a great chance to learn from other people's work and reflect on your own work. Submit one combined review to the [external peer review assignment](https://www.gradescope.com/courses/827978/assignments/5392834){:target="_blank"} on Gradescope by **11:59pm on December 6**. Remember to add your group members on your submission.

<a name = 'final-project-report'></a>

## Final Project Report (50%) - December 13, 2024

**The project submission should include the following four components, submitted across three Gradescope assignments.** For all three assignments, submit one per group. Make sure to add your group members on the Gradescope submission.

**Please submit component 1 as a zip file to the [final project code submission assignment](https://www.gradescope.com/courses/827978/assignments/5412929){:target="_blank"} on Gradescope.** Please make sure the folder in the zip file has the following structure:

```
[your studentIDs joined by _]/
    data/[all datasets used]
    analysis/[analysis notebooks]
    narrative/[narrative PDF]
    figures/[figures included in the narrative PDF]
```

Please use student IDs joined by `_` as the name for the top-level directory. The analysis notebooks must be runnable within this directory structure. If the narrative PDF includes any figures that are created in the analysis notebooks, the figures should be saved to `figures/` by the analysis notebooks.

**Please also submit components 2-3 as a PDF to the [final project report submission assignment](https://www.gradescope.com/courses/827978/assignments/5045744){:target="_blank"} on Gradescope.** Make sure that the link to the video is included somewhere in your PDF.

**For component 4, you will submit your test set predictions to the [NLP predictions assignment](https://www.gradescope.com/courses/827978/assignments/5159424){:target="_blank"}.** See below for more details.

### [Component 1] Analysis Notebooks (10%)

This component includes all the Jupyter Notebook(s) containing all the analyses that you performed on the datasets to support your claims in your write-up. Make sure that all references to datasets are done as `data/[path to data files]`. By running these notebooks, we should be able to replicate all the analysis/figures done in your write-up.

Your analysis notebook(s) should address all of the following components in the data science lifecycle. Please note that a thorough explanation of your thought process and approach is **as important as** your work. Unreadable/uncommented code will lose points. Along with the code for the EDA portion (which also has to be included), we have provided a few additional preliminary questions/tips you can consider for the modeling portion of the project:

  - Which model(s) do you use and why?
  - How do you use your data for training and testing?
  - Does your model require hyperparameter tuning? If so, how do you approach it?
  - How do you engineer the features for your model? What are the rationales behind selecting these features?
  - How do you perform cross-validation on your model?
  - What loss metrics are you using to evaluate your model? Why?
  - From a bias-variance tradeoff standpoint, how do you assess the performance of your model? How do you check if it is overfitting?
  - How would you improve your model based on the outcome?
  - Are there any further extensions to your model that would be worth exploring?

| Criterion                                             | Points|
|-------------------------------------------------------|-------|
| Code readability and documentation                    | 3     |
| Proper and sufficient utilization of Python libraries | 2     |
| Overall code quality                                  | 2     |
| Replicability of the results                          | 3     |
| **Total**                                             | **10**|

### [Component 2] Project Write-Up (20%)

This is a single PDF that summarizes your workflow and what you have learned. It should be structured as a research paper and include a title, list of authors, abstract, introduction, description of data, methodology, summary of results, discussion, conclusion, and references. Make sure to number figures and tables, include informative captions, and ensure you include the provenance of the figures in the main narrative. We encourage you to render the PDF using LaTeX, but we will not be able to provide assistance with LaTeX-related issues.

Specifically, you should ensure you address the following in the narrative:

* Introduction: ensure you include a brief survey of related work on the topic(s) of your analysis. Be sure to reference current approaches/research in the context of your project, as well as how your project differs from or complements existing research. You must cite all the references you discuss in this section.
* Description of data: ensure you outline the summary of the data and how the data was prepared for the modeling phase (summarizing your EDA work). If applicable, descriptions of additional datasets that you gathered to support your analysis may also be included.
* Methodology: carefully describe the methods/models you use and why they are appropriate for answering your research questions. You must include a detailed description of how modeling is done in your project, including inference or prediction methods used, feature engineering and regularization if applicable, and cross-validation or test data as appropriate for model selection and evaluation. You may also include interesting findings involving your datasets.
* Summary of results: analyze your findings in relation to your research question(s). Include/reference visualizations and specific results. Discuss any interesting findings from your analysis. You are encouraged to compare the results using different inference or prediction methods (e.g. linear regression, logistic regression, or classification and regression trees). Can you explain why some methods performed better than others?
* Discussion: evaluate your approach and discuss any limitations of the methods you used. Also, briefly describe any surprising discoveries and whether there are any interesting extensions to your analysis.

The narrative PDF should include figures sparingly to support specific claims. It can include a few runnable code components, but it should not have large amounts of code. The length of the report should be 8 ± 2 pages when it is printed as a PDF, excluding figures and code.

Tip: if you need to write a large amount of LaTeX on markdown, you may want to use the `%%latex` cell magic. However, we also encourage you to explore [Overleaf](https://www.overleaf.com){:target="_blank"} for easily writing clean LaTeX documents.

| Criterion                                                              | Points|
|------------------------------------------------------------------------|-------|
| Exploratory data analysis                                              | 3     |
| Modeling and inference techniques                                      | 6     |
| Analysis of results                                                    | 5     |
| Implementation of peer review feedback                                 | 2     |
| Discussion of potential societal impacts and/or ethical concerns       | 2     |
| Overall clarity and structure of the report                            | 2     |
| **Total**                                                              | **20**|

### [Component 3] Video Recording (10%)

The presentation video should provide an overview of your project, highlighting the main points outlined in the write-up. The video should be approximately 5-7 minutes long but can extend up to 10 minutes. You should upload your video to YouTube and include the YouTube link in your final project write-up.

### [Component 4] Test Set Performance (10%)

This component of the final report will be graded based on your models' performance on the test set for both tasks of your chosen project (please find the thresholds for each task in the rubrics). You will need to submit your predictions to Gradescope to get your test performance; you will be allowed to upload up to 4 times a day. Please find the test data for each task below.

The test sets for both tasks are named as follows:

1. `arena-test-set-prompt-and-responses.jsonl.gz`
2. `arena-test-set-prompts-embeddings.npy`
3. `arena-test-set-model_a_response-embeddings.npy`
4. `arena-test-set-model_b_response-embeddings.npy`
5. `arena-test-set-topic-modeling.jsonl.gz`

All files are located in `shared/course/data100-shared-readwrite/fa24_grad_project_data/nlp-chatbot-analysis_data/test-set` directory on Data 100 Datahub.

Submit a single CSV file with three columns named `question_id`, `winner`, `hardness_score` to [the predictions assignment](https://www.gradescope.com/courses/827978/assignments/5159424){:target="_blank"}.

The maximum for each task is 5 points; please see the thresholds for the tasks below.

| Task (metric)     | Threshold | Points |
|-------------------|-----------|--------|
| Task A (accuracy) | 0.50      |   3    |
|                   | 0.52      |   4    |
|                   | 0.54      |   5    |
| Task B (MSE)      | 2.78      |   3    |
|                   | 2.64       |   4    |
|                   | 2.5       |   5    | 
