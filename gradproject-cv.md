---
layout: page
title: CV Graduate Project
nav_exclude: true
description: Specifications for the CV grad project for Data 200.
markdown: kramdown
---

{: .warning }
⚠️ This content is archived as of March 2026 and is retained exclusively for reference. [Find current offerings.](https://ds100.org/)

# Graduate Project 1: Computer Vision
{:.no_toc}

* TOC
{:toc}

## Project Description: Computer Vision

In disaster situations, it is important for emergency response efforts to have access to quick and accurate information about an area in order to respond effectively. This project will explore how data science techniques can be useful for such efforts.

### Project Goals
{:.no_toc}

- Learn to work with image data by learning to use common feature extraction techniques like Sobel edge filtering.
- Learn to work on real-world data with common complexities such as class imbalance, low signal-to-noise ratio, and high dimensional data.
- Learn how to design effective preprocessing and featurization pipelines for solving difficult machine learning tasks.

### Mission
{:.no_toc}

You have been hired by a crisis response agency to help assist them with your impressive data science skills! The agency has found that using satellite imagery is highly useful for supplying information for their response efforts. Unfortunately, however, annotating these high-resolution images can be a slow process for analysts. Your mission is to help address this challenge by developing an automatic computer vision approach!

### Dataset Description
{:.no_toc}

The agency would like you to develop your approach on their internal dataset, derived from the [xView2 Challenge Dataset](https://xview2.org/){:target="_blank"}. This dataset contains satellite images of buildings after various natural disasters. The buildings are labeled based on the level of damage sustained on a scale ranging from 0 (no damage) to 3 (destroyed).

You can access all of the data within the `./satellite-image-data` directory. The dataset consists of the following folders for different natural disasters:
1. `midwest-flooding`
2. `socal-fire`
3. `hurricane-matthew`

Within each folder is a zip file `train_images.npz` containing the satellite images as numpy arrays and a `train_labels.npy` file with corresponding damage level labels.

> Testing: In the main directory, there are also the `test_images_hurricane-matthew.npz` and `test_images_flooding-fire.npz` zip files. The first contains test images from the `hurricane-matthew` disaster and the latter consists of a combination of test images from `midwest-flooding` and `socal-fire`.

## Action Items

You are required to perform **(1) Exploratory Data Analysis (EDA)** and **(2) Modeling (Task A and Task B)** for this project.

### Exploratory Data Analysis

To help you with onboarding, the agency has provided a starter notebook [`cv_eda_starter.ipynb`](https://data100.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FDS-100%2Ffa24-student&urlpath=lab%2Ftree%2Ffa24-student%2Fgrad-proj%2Fsatellite-images%2Fcv_eda_starter.ipynb&branch=main){:target="_blank"} which will introduce you to the dataset and some useful internal tools. After completing the onboarding assignment you will be comfortable with the following:

1. Loading and visualizing data using tools from `data_utils.py`
2. Processing different color channels in the dataset images.
3. Extracting feature information from images using tools from `feature_utils.py`.

The agency would like you to start performing some exploratory data analysis to build an initial understanding of the data. As part of the exploratory data analysis, the agency is interested in understanding certain aspects of the dataset better. Specifically, they are looking for:

- Basic statistics about the dataset, such as the number of images per disaster type and the distribution of image sizes and damage labels.
- Insights into useful image features for classifying images based on disaster type or damage level. Previous interns have found color information to be potentially useful. You are tasked with verifying this and exploring whether color features can effectively differentiate:
    - `midwest-flooding` from `socal-fire` images.
    - Damage levels 1 and 3 within the `hurricane-matthew` dataset.

Please prepare an EDA report to present to the agency leadership with the above in mind. See below in the description for [Milestone 2](#milestone-2-eda) for detailed instructions for the report.

### Project Tasks

Now that leadership is pleased with your initial EDA report and confident in your data science ability, they would like you to assist the agency with various tasks. *Please complete Task A first and then Task B.* To help you get started, the agency has provided a starter notebook [`cv_model_starter.ipynb`](https://data100.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FDS-100%2Ffa24-student&urlpath=lab%2Ftree%2Ffa24-student%2Fgrad-proj%2Fsatellite-images%2Fcv_model_starter.ipynb&branch=main){:target="_blank"}

#### *Task A: Disaster Type Classification*
{:.no_toc}
The agency consists of different subdivisions for assisting with different disaster types, e.g., fires, floods, etc. In the event of a disaster, the agency mounts its response effort by first assessing the type of disaster and then requesting the appropriate subdivision to assist with the disaster.

Your task is to assist the agency with making this initial call quickly by automatically classifying images based on the disaster scenario. Specifically, your role will be to build a classifier that can distinguish images from the `midwest-flooding` disaster and the `socal-fire` disaster.

To assess your performance, please submit predictions for the `test_images_flooding-fire.npz` images. This should be in a csv file `test_images_flooding-fire_predictions.csv` consisting of a single column named `pred`, with a 0 to indicate a `midwest-flooding` prediction and a 1 to indicate a `socal-fire` prediction. The prediction in row *i* should correspond to the *ith* image.

#### *Task B: Damage Level Classification*
{:.no_toc}
The agency needs to know how severe a disaster is in order to allocate resources for a response effectively. The agency is especially concerned with human lives and uses building damage as an important metric for disaster severity.

Your task is to assist the agency by automatically detecting the building damage level after a disaster. Specifically, create a damage level classifier for the `hurricane-matthew` disaster.

To assess your performance, please submit predictions for the `test_images_hurricane-matthew.npz` images. This should be in a CSV file `test_images_hurricane-matthew_predictions.csv` consisting of a single column named `pred`, with a 0-3 prediction of the damage level. The prediction in row *i* should correspond to the *i*th image.

#### Resources
{:.no_toc}
To assist you in your efforts the agency has compiled the following list of resources:
- For more background about the dataset you can look at the [paper](https://arxiv.org/pdf/1911.09296.pdf){:target="_blank"} associated with the dataset.
- For image processing, [scikit-image](https://scikit-image.org/){:target="_blank"} is a very useful library. This [tutorial](https://www.kaggle.com/code/bextuychiev/full-tutorial-on-image-processing-in-skimage){:target="_blank"} may be helpful for learning how to use the library.
- For problems with imbalanced classes, the [imblearn](https://imbalanced-learn.org/stable/index.html){:target="_blank"} library has useful tools and examples.

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

  - Number of images per disaster.
  - Image sizes in each dataset. Should ideally observe large variance in sizes, but similar distribution for each disaster.
  - Damage labels. Should observe imbalances in the labels.
  - (Open-ended) Visualize the distribution of color for different disasters.
  - (Open-ended) Convey that the distributions are “separable” somehow.

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

Submit to the [first draft project report assignment](https://www.gradescope.com/courses/827978/assignments/5045727/){:target="_blank"} on Gradescope by **11:59pm on December 2**.

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

**For component 4, you will submit your test set predictions to the [CV predictions assignment](https://www.gradescope.com/courses/827978/assignments/5159453){:target="_blank"}.** See below for more details.

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

`test_images_flooding-fire.npz` is the test for Task A and `test_images_hurricane-matthew.npz` is the test set for Task B; both files are located in `shared/course/data100-shared-readwrite/fa24_grad_project_data/satellite-image-data` directory on Data 100 Datahub.

Please submit two CSV files named `test_images_flooding-fire_predictions.csv`, and `test_images_hurricane-matthew_predictions.csv` to [the predictions assignment](https://www.gradescope.com/courses/827978/assignments/5159453){:target="_blank"}. Each CSV should only contain one column named `pred`.

The maximum for each task is 5 points; please see the thresholds for the tasks below.

| Task (metric) | Threshold | Points |
|---------------|-----------|--------|
| Task A (accuracy) | 0.8131  |   3    |
|               | 0.9093  |   4    |
|               | 0.9800  |   5    |
| Task B (F1 score)  | 0.3987  |   3    |
|               | 0.4334  |   4    |
|               | 0.5300  |   5    |
