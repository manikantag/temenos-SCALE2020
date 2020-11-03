# Module 4: Model life cycle and monitoring

**Duration**: 15 mins

**Prerequisite Software and Tools**

- Browser & Internet Access
	
Tasks:	In this module you will learn about a model’s life cycle in the context of your Organisation, and how to monitor its performance over time

## Module 4: Lab Instructions

1. **Model life cycle in Temenos XAI Platform**
A model’s life cycle and its current state are represented in the “Life Cycle” section of your model. The screen depicts these, as well as the log related to previous actions executed on the model. The life cycle is designed to allow multiple people to work in parallel on the same project, flagging some of them as potential candidates to be used in production, accepting/rejecting, deploying, etc. For the full picture regarding model life cycle, please refer to the documentation. 
NOTE: Please remember that, in order to receive/respond API calls, a model has to be in either “Deployed” or “Live” state.

image044

2. **Monitoring model’s performance – Bulk Inference**

(I)
A bulk inference is a process where you will upload a csv file containing data rows. These rows will be evaluated with your model, which will provide a score, a bucket (if a default bucketing is configured) and other errors and/or warnings that may have prevented the row evaluation. The uploaded file must contain at least the same columns/features the model needs to evaluate every instance. It can contain extra columns, which will be simply ignored. Results of a bulk inference can be downloaded as a CSV or Excel file. 
To perform a Bulk Inference, choose the model you have decided to work on, go to “Bulk Inference” under “Population Evaluation”. For this use case, use the provided file called “Lending-club-sampled-for-BI.csv”. This file is just a sample of the original we used to build the models. 
Then press the “Create New Bulk Inference” button. 

image046

(II)
Once the Bulk Inference job is finished, you will see a summary screen presenting the statistical results, like the one you can see after building a model. 

image048
 
3.	**Population Stability and Characteristic Stability**
A previously run Bulk Inference can be used to perform Population and Characteristic Analysis. Doing so will populate the tabs “Population Stability” and “Characteristic Stability” you can find in a Bulk Inference.
- For the “Population Stability”, the uploaded file does not need to contain the target outcome. It measures how different the distributions of the input features are, comparing the original data used to build the model, and the data contained in the bulk inference file.

image050

- For the “Characteristic Stability”, the uploaded file must contain the target outcome. This will compare the model’s performance on the original data and the data contained in the bulk inference file.

image052

If results for these analysis are very different, that might indicate the population we are evaluating through the bulk inference is very different to the one the model was built upon and, therefore, it might not be safe to go on using the model and refreshing it might be a good idea. 
 
**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey](xx)