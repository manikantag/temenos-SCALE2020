# Module 6: Actionable Insights

**Duration**: 15 mins

**Prerequisite Software and Tools**

- Browser & Internet Access
	
Tasks:	In this module you will learn how to harness XAI models and their explainability to evaluate “what if” scenarios.

## Module 6: Lab Instructions

1. **Borderline decision – Can I change anything?**

In this example I will focus on an instance which is a borderline decision, it is, classified as “Uncreditworthy” but with a borderline score. As my model and yours will be different, you can’t see the same instance as I do, but just look for any example which has an “Uncreditworthy” score just above 50%.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image064.png)

2.	**Negative feature contribution – FICO Credit Score**

Having a look at the rules and drivers view, I noticed that “FICO Credit Score is medium” is contributing negatively to a decision.  

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image066.png)

3. **What if I changed the value?**
Let’s assume the client aplying for the loan has some outstanding debt, lowering significantly his FICO Credit Score and, could the client pay such debt, the credit score value would go back to normal. 
We can evaluate this hypothetical scenario: what if the client could settle their debt and raise their FICO credit score? For the specific instance you are exploring, click on the button “Open in Inference” at the top right-hand side of the screen. A new page will be opened, displaying a form containing all feature values for the instance we are exploring. Now I can manually change the value of FICO credit Score to a hypothetical one and see what the model would evaluate in this new case by clicking the “Predict” button. 
As you can see in the following images, slightly raising this value changes the decision from “Uncreditworthy” to “Creditworthy”, giving you the chance to write more business as a loaner and your client the chance to get the loan. 
NOTE: for the evaluation to happen, your model has to be deployed. 
As you will be exploring a different instance, the value you might need to change in order to switch the decision might be different. Feel free to explore and play around with the form and the different values to change your prediction. 

(I) 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image068.png)

(II)

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%201%20-%20XAI%20Models/images/image070.png)
 
**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey](xx)