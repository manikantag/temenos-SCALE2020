**Assess the Score and Update the Loan Application**

Now that we have the score from the credit bureau, let's see if our business rules consider the applicant to be creditworthy or not.

We'll add a Business Rule that assesses whether the credit score is so good that the loan can be approved without further diligence, or whether it is so bad that it must be rejected right away. The rule will also determine that any score in between will require a credit analyst to have a closer look at the case.

1. Navigate to Configure Services » Rules and click on the `LoanApprovalRules(1.0)` rule set and then on the `assessScore` operation. The field Rule Logic shows how the rule is defined. Click on the Expand icon to examine it better. You may recognise the syntax is [MVEL](http://mvel.documentnode.com/), which in turn is based on YAML. Read more about Fabric Business Rules [here](https://docs.kony.com/konylibrary/integration/kmf_integrationservice_admin_console_userguide/Content/Rules_Services.htm).

```
---
name: Poor
condition: score < 600
actions:
- results.addParam("decision", "Rejected")
---
name: Good
condition: score >= 600 && score <= 699
actions:
- results.addParam("decision", "Review")
---
name: Excellent
condition: score >= 700
actions:
- results.addParam("decision", "Approved")
```

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image098.png)


**Note**: The basic structure of Business Rules is that they can evaluate logical conditions on their input parameters, and execute actions based on those. In this case, the `score` input parameter is being evaluated in each rule’s `condition` against the ranges under 600, 600-699 and above 700. In each case, the `actions` for the rule add a decision to the output of the rule.

2. Go back to Apps in the Fabric Console, open the Fabric app you are working on, navigate to Configure Service » Workflow and click on the `LoansApplicationWF` workflow.

3.	Add a `Business Rule` task between the `Get Credit Score` service task and the `Update Application` service task. Disconnect and reconnect the flow arrows accordingly.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image100.png)

4.	Click the newly added business rule, open the properties tab to the right and name it `Assess Score`.

5.	Select `LoanApprovalRules(1.0)` as the Rule Set.

6.	Select `assessScore` as the business rule.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image102.png)

7.	Click to configure the Input Parameters, add an input `score` from `FABRIC_WORKFLOW_CONTEXT` and type in `credit.score`. This takes the score we got from the credit bureau from the workflow's context and passes it to the business rule's `score` input parameter. Click SAVE to close the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image104.png)

8.	Click to configure the Output Parameters, and type in `rule1` (or something else of your choosing) as the namespace to store the output of this service. Click SAVE to close the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image106.png)
 
**Note**: This means that if this service responds with `{"decision": "Approved", "opstatus": 0}`, we can later refer to `rule1.decision` and get the `Approved` value.

9. Click the `Update Application` service task and click to configure the Input Parameters. You will see the mappings for the `id` and `score` fields which we added in a prior step.

10.	Add a new mapping of `rule1.decision` from the `FABRIC_WORKFLOW_CONTEXT` to the `status` field in the model.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image108.png)

11.	Click the SAVE button in the modal and then click the SAVE button in the bottom right corner of the Console.

**Test Our Progress So Far (Optional)**
If you wish, repeat the instructions earlier to publish and test your progress so far. If you do, you will see that every new loan application you create will have its `status` field updated to `Approved, Review` or `Rejected`, based on how the `assessScore` rule evaluates the `score` returned by the credit bureau.

**Send an Approval Notification**
If the applicant's score is good enough to approve right away, we should send out a notification.

1. Add an `Exclusive Gateway` just before the `End` event and reconnect the arrow flows as required.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image110.png)

2.	Click the new gateway, click the Properties tab to the right and name it `Gateway1`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image112.png)
 
3.	Add a `Message` event onto the canvas right between `Gateway1` and the End event. Click the properties tab to the right and name it `Notify Approval`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image114.png)

4.	Select the new `Notify Approval` message event, click the arrow, and from the Properties tab to the right, name it `isApproved` and click the ADD button under Entry Validation Criteria.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image116.png)
 
5.	Click the Add Condition button, select `FABRIC_WORKFLOW_CONTEXT`, type `rule1.decision` for the left-hand value, select the `==` operator, select `none` for the context and type `Approved` for the right-hand value, and click the SAVE button on the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image118.png)
 
6.	Click on the `Notify Approval` event, click the COMPOSE EMAIL button from the Properties tab to the right and set the following values.

**To**	$email
**Subject**	Your loan has been approved!
**Body**	Dear $firstName,`<br>`We're pleased to inform you that your loan has been `<b>`approved!`</b>`

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image120.png)

7. Click the Parameters tab on the right side of the modal and add the following mappings and click the SAVE button on the modal:

- Map `email` from `BACKEND_RESPONSE` to `email`.
- Map `firstName` from `BACKEND_RESPONSE` to `firstName`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image122.png)

**Send a Rejection Notification**
If the applicant's score is bad enough to approve right away, we should send out a notification.

1. Add another `Message` event onto the canvas. Click the properties tab to the right and name it `Notify Rejection`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image124.png)

2. Drag a new arrow from `Gateway1` to the new `Notify Rejection` message event, click the arrow, and from the Properties tab to the right, name it `isRejected` and click the ADD button under Entry Validation Criteria.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image126.png)

3. Click the Add Condition button, select `FABRIC_WORKFLOW_CONTEXT`, type `rule1.decision` for the left-hand value, select the `==` operator, select none for the context and type `Rejected` for the right-hand value. Click the SAVE button on the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image128.png)

4.	Click on the `Notify Rejection` event, click the COMPOSE EMAIL button from the Properties tab to the right and set the following values.

**To**	$email
**Subject**	Your loan has been rejected
**Body**	Dear `$firstName`,`<br>`We regret to inform you we `<i>cannot</i>` approve your loan application at this time.

6. Click the Parameters tab on the right side of the modal and add the following mappings and click the SAVE button on the modal:

- Map `email` from `BACKEND_RESPONSE` to `email`.
- Map `firstName` from `BACKEND_RESPONSE` to `firstName`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image130.png)

7. Add an `End` event just after the `Notify Rejection` event and click the SAVE button on the bottom right corner.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image132.png)

**Make Room for a Human to Decide**

If the applicant's score is neither too good nor too bad to make an automatic decision, we need human intervention —e.g.: from a credit analyst— to decide.

1. Add a new `User Task` activity, click the Properties tab and name it `Review Case`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image134.png)
 
2. To specify that after reviewed an application must be either approved or rejected, set the Valid state transitions field to `Approved, Rejected`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image136.png)
 
3. Connect `Gateway1` to the newly added `Review` activity. Click the connecting flow, click the Properties tab to the right, name it `needsReview` and click the ADD button under Entry Validation Criteria.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image138.png)
 
4. Click the Add Condition button, select `FABRIC_WORKFLOW_CONTEXT`, type `rule1.decision` for the left-hand value, select the `==` operator, select `none` for the context and type `Review` for the right-hand value. Click the SAVE button on the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image140.png)

- Note: With this, we've covered all the three possible scenarios for `Gateway1` based on the value of the application model's `status` field.

**Send the Final Notification Either Way**

Let's reuse the existing `Message` events.
1. Add a second `Exclusive Gateway`, name it `Gateway2` and connect the `Review Case` task to it.
 
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image142.png)

2.	Connect `Gateway2` to the already existing `Message` event called `Notify Approval`. Select the new arrow, click the Properties tab to the right and name it `isReviewedAndApproved`.
 
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image144.png)

3. Click the ADD button under Entry Validation Criteria, click the Add Condition button, select `BACKEND_RESPONSE`, type `status` for the left-hand value, select the `==` operator, select `none` for the context and type `Approved` for the right-hand value. Click the SAVE button on the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image146.png)

4. Connect `Gateway2` to the already existing `Message` event called `Notify Rejection`. Select the new arrow, click the Properties tab to the right and name it `isReviewedAndRejected`.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image148.png)

5.	Click the ADD button under Entry Validation Criteria, click the Add Condition button, select `BACKEND_RESPONS`, type status for the left-hand value, select the `==` operator, select none for the context and type `Rejected` for the right-hand value. Click the SAVE button on the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image150.png)

6. Verify the end-to-end workflow looks like the one below and click the SAVE button on the lower-right corner.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image152.png)
 
**Test the Whole Thing (Optional)**

Let's first test a loan application by a borrower with an excellent credit score. In this case the application will be approved automatically. Then, we'll test another loan application by a borrower with a poorer score. A credit analyst will then manually reject the application.

1. Click the Publish tab under the `LoanOrigination1` Fabric app, check the box next to an environment and click the PUBLISH button in the bottom right corner. Wait until the Console shows the status is `Published`. You will see the application's primary and secondary app keys and secrets listed below.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image154.png)
 
2.	Click the Object Services icon just below the name of the environment. This will open a new tab to the Fabric Runtime's Console in the Object Services. This will show all the object services published. You should see the `LoanApplicationObjS` service.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image156.png)
 
3.	Click the dropdown under the App Data Model Objects column in the `LoanApplicationObjS` row and select the `ApplicationModel`. This will display Request Input and Request Output tabs.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image158.png)
 
4. In the Request Input tab, select the `create` operation from the dropdown and paste this in the Body of the request:

```
{
	"idDoc": "123-1234-002",
	"status": "New",
	"firstName": "Tywin",
	"lastName": "Lannister",
	"email": "[an email address for testing]"
}
```

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image160.png)

6. This will return a response that looks like the one below. Make a note of the `id` value.

```
{
    "id":"[number]","opstatus":0,"httpStatusCode":0
}
```
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image162.png)

7. Repeat step #5 and #6 with this payload:

```
{
	"idDoc": "123-1234-005",
	"status": "New",
	"firstName": "Jon",
	"lastName": "Snow",
	"email":"[an email address for testing]"
}
```

8.	Now select the `get` operation and click the Get Response button to verify that both applications have been created. You’ll notice that Tywin has such a good score that his application has been approved automatically. Whereas Jon does not have such a good score and so the case needs further review.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image164.png)

9.	Click the Workflow Services option from the main menu to the left, and then select `LoansApplicationWF`. You should see two newly fired workflow executions for each of the loan application you've just created. The first one —Tywin's— will be `COMPLETED`. The second one —Jon's— will be `RUNNING`. The `RUNNING` status of Jon’s application means it’s still waiting for a human to take action.
 
 ![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image166.png)

10.	Out of the two newly fired workflow executions, click on Tywin's application. You should see that the status for all the actions is `DONE`. If the execution is not done, it might be still running but will finish shortly. Click the Refresh button. 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image168.png)

**Note**: If the notification step shows `FAILED`, go back and check your workflow is well defined, and make check the Email Configuration in your Engagement Services.

Go back to the list of the executions of `LoansApplicationWF` and click on Jon's application. You should see that the status of the last action is `PAUSED`. This means that the workflow is waiting for a human to intervene.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image170.png)

11.	Now let's simulate a credit analyst's approval. Click the Object Services option from the main menu to the left, click the dropdown under the App Data Model Objects column in the `LoanApplicationObjS` row and select the `ApplicationModel`.

12. In the Request Input tab, select the update operation from the dropdown —This will fire an `HTTP PUT` operation. Paste this in the Body of the request:

```
{
	"id": [the id of Jon's application],
	"status": "Rejected",
	"firstName": "Jon",
	"lastName": "Snow",
	"email":"[an email address for testing]"
}
```
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image172.png)

14.	This will return a response saying that one record has been updated.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image174.png)
  
15.	Go back to Workflow Services and click `LoansApplicationWF`. You should now see Jon's application is also in `COMPLETED` status. Click on it and verify that all activities are in `DONE` status.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image176.png)

16.	Check the inbox of the email address you're using for testing. You should have received emails notifying you of the results of both loan applications.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%206%20-%20Intro%20to%20Quantum%20Fabric/assets/image178.png)
 
**A Final Word on Workflows**
During this lab you’ve designed, published and tested a workflow. As you will have been able to appreciate, workflows are advanced tools that build on top of other Fabric constructs, such as Integration Services, Object Services, Business Rules and Engagement Services. If you’ve struggled with these concepts we recommend you go back and explore the labs and other enablement materials that go over these other features in more detail.
Also, workflows are very powerful tools that will allow you to decouple client apps from business processes. If used right, Fabric Workflows could allow you to change processes without affecting the client applications or having to distribute new versions of them. They could also allow you to start a user journey on one device, continue on a second device and finish on a third one. 
However, workflows should not be abused. Not everything in your app is necessarily a good candidate to be modelled as a Fabric Workflow. Some use cases may be too simple or trivial to become workflows. Meanwhile, others may be way too large or complex. Fabric Workflows are meant as a lightweight solution for use cases which commonly arise when building multi-experience digital experiences, but not as a fully-fledged BPMS for the entire enterprise.

**Module 3: Lab Summary**
During this lab you’ve designed, published and tested a workflow. As you will have been able to appreciate, workflows are advanced tools that build on top of other Fabric constructs, such as Integration Services, Object Services, Business Rules and Engagement Services. If you’ve struggled with these concepts we recommend you go back and explore the labs and other enablement materials that go over these other features in more detail.

Workflows are very powerful tools that will allow you to decouple client apps from business processes. If used right, Fabric Workflows could allow you to change processes without affecting the client applications or having to distribute new versions of them. They could also allow you to start a user journey on one device, continue on a second device and finish on a third one. 

However, workflows should not be abused. Not everything in your app is necessarily a good candidate to be modelled as a Fabric Workflow. Some use cases may be too simple or trivial to become workflows. Meanwhile, others may be way too large or complex. Fabric Workflows are meant as a lightweight solution for use cases which commonly arise when building multi-experience digital experiences, but not as a fully-fledged BPMS for the entire enterprise.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()