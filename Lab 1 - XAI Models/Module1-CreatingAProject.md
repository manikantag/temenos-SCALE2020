# Module 1: Creating a project (xAI)

**Duration**: 15 mins

**Prerequisite Software and Tools**

- Browser & Internet Access

Tasks: In this module you will be creating a binary classification project from a CSV file and making sure it is ready to work with.

## Module 1: Lab Instructions

1. Landing page and create new project

After login in into the Platform, you’ll be redirected to the landing page, where you can see all previously created projects. Your environment might be empty (i.e. no previous projects created). In order to create a new project, click on the “New Project” button.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image006.png)

2.	Upload Wizard
*(I)*
The upload wizard will start. You can either choose a local file using the “Upload File” button, or you can choose a previously uploaded file from the list. Use the “Lending Club.csv” file you have been provided with. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image008.png)

*(II)*
The platform will automatically detect the columns present in your file. You can manually select/deselect them to prevent some of them (which might not be useful, as unique IDs) from being uploaded upfront. For the Lending Club use case we will focus on, leave all columns selected. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image010.png)

*(III)*
The next screen in the Wizard requires you to specify the problem type your dataset represents, and what’s the target column that needs to be predicted. Choose “Binary Classification” and “Class”, respectively. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image012.png)

*(IV)*
In the next screen you can choose a name for your project. You can also set up upfront some encoding options that are out of the scope of this lab. You can refer to the documentation for more information about them. Click “Create” once you have chosen a name for your project. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image014.png)

3	**Project overview**
The “Overview” page just highlights some relevant information about the project you have just created. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image016.png)

4	**Audit**
The dataset you will be using, Lending Club, is a very well curated dataset and should not flag any warnings, so the screenshot attached here belongs to a different dataset and only has illustrative purposes. The Platform can automatically detect some issues related to the dataset: perfectly correlated columns, columns containing a single value or being completely blank, etc. This issues can be manually addressed one by one or handled automatically by the Platform using the “Auto-Fix All” button. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image018.png)

5	**Partitioning**
When building a predictive model, the available data is usually split into three different subsets: training (the one used to fit the model), validation (used to prevent overfitting during the training process) and testing (unseen data to assess model performance once it is built). The “Partitioning” tab under the “Data Source” section allows you to configure the size of these subsets. The rest of the options can be looked up in the documentation. 
For the purpose of this lab you can just leave the default configuration.  

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image020.png)

**Module 1: Lab Summary**

In the first module we created a project, explored the audit warnings and set up the partitioning, so we are ready to start working on choosing the right features to build our models afterwards.

At this point we will move on to [Module 2](xx) where we will focus on selecting features.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey](xx)