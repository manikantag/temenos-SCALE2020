# Module 3: Building models – Focus on XAI

**Duration**: 15 mins

**Prerequisite Software and Tools**

- Browser & Internet Access

Tasks: In this module you will be creating features sets, both manually and through feature selection, in order to build models. 

## Module 3: Lab Instructions

1. **Building models in 1-click**
After finishing with our feature sets, it’s time to build models. Go to the “New Model” screen under “Intelligence Task”. Make sure you choose the right feature set to work with; you can choose the “Base features” set or some other else you have defined in previous steps. 
If, as a user, you have limited knowledge about data science, just click on which model type and how many of them you want to build, and the default configuration will be used. If you want a more experienced approach, feel free to explore the “Configuration” button for each model type. Do not hesitate to visit the documentation for extra details about the parameters. 
Click on “Start Model Build” to run jobs for each model you want to build. 

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image032.png)

2. **Configuring the hyperparameters (Fuzzy Logic)**
As we will focus our attention on Fuzzy Logic models (as they provide XAI capabilities) please feel free to have a closer look at the parameters defining these models. 

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image034.png)

3. **Model Summary**
Once the job have run successfully and the models have been built, you can see all built models under the “Models” section within your project. 
For each model you will find a screen summarizing some statistical and scientific metrics representing its performance. Please refer to the documentation for extra details on how to assess model quality.
As a tip, when building fuzzy logic models, you might be willing to have a model that has a high average recall, but also not very imbalanced recalls in both classes (“Creditworthy” and “Uncreditworthy”). 
In order to progress within this lab, make sure you choose a model to keep working on it.

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image036.png)

4. **Bucketing**
(I)
The bucketing widget allows the user to explore how the model is capturing the likelihood of a model event happening (in this case, an “Uncreditworthy” instance) according to the score obtained in the instance evaluation. 
In the context of your model, go to the “Bucketing” section and click on “New bucketing”. 

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image038.png)

(II)
Select the file to use in the bucketing, assign a name to it and click on “Create New Bucketing”. For illustrative purposes, we will be using the same original file “Lending Club.csv” to perform the bucketing. 

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image040.png)

(III)
After the job is completed, the resulting bucketing is displayed. The graph represents as a stacked histogram the Creditworthy/Uncreditworthy instances (in blue/red, respectively) in each score range. The green light represents the default rate, i.e., the proportion of Uncreditworthy applications in each score bucket. As you can see in the image below, the higher the score, the higher the default rate, therefore increasing the probability of default. This means our model is capturing the right trend, and a higher score for the Uncreditworthy class implies a higher chance of payment default for the applicant. 
The bucketing widget can be used, for instance, as a pricing strategy: as a business owner, I can apply a higher interest rate to higher buckets, to account for the extra risk I take by lending money to those applicants with higher scores. Therefore, this tool allows you to assess how using this model can impact your business. 
The bucketing is configurable: you can change the number of buckets and the thresholds separating them. 
In addition, deployed models are recommended to have a “default bucketing” configured, so the bucket an instance belongs to will be part of the API response. 

![image](https://github.com/temenos/SCALE2020/blob/main/Training%20and%20Deploying%20Models%20with%20Temenos%20AI%20Platform/images/image042.png)

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey](xx)