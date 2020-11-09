# Module Three: Creating a Quantum Fabric Workflow
**Duration**: 30 mins

**Prerequisite Software and Tools**

- The file [LoansOrigination1.zip](https://community.kony.com/downloads) containing the Fabric application we'll use for this lab.

- a developer account at http://Manage.kony.com

Tasks you will complete in this lab exercise include:

- Import a Fabric app which includes:
    - An Object Service called `LoanApplicationObjS.`
    - A Business Rule Set called `LoanApprovalRules.`
    - A Mock Integration Service called `CreditBureauMock.`
    - Create a new Workflow based on the previously existing services mentioned above.
    - Publish the newly created workflow.
    - Test the newly created workflow.

## Module 3: Lab Instructions

**Optional**

Only the steps in this lab titled with the word “Optional” will require the following:

- A Fabric Runtime Environment 9.1+: In order to be able to publish a workflow you will need a paid-for Fabric account. If you do not have access to a paid-for account, you can still do this lab and follow along the steps to design a Workflow, but you will not be able to publish it.

- Engagement Services 9.1+ with previously configured email settings and an email address for testing

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/57.EngagementServices.png)

**Import the Fabric App**

1. Log into manage.kony.com.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/58.QuantumApps.png)

2. Click on Apps option on the main menu to the left and click the IMPORT button.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/59.FabricApps.png)

3. Browse your file system and select the zipped Fabric bundle called `LoansOrigination1(v1.0).zip` as a new application.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/60.LoansOrigination1.png)
![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/61.LoansOrigination2.png)

*Note*: Make sure you give it a name that will tell it apart from the applications created by your peers during this lab - e.g.: Append your initials to the name of the application.

4. Verify that the new Fabric app `LoansOrigination1` is imported.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/62.FabricAppsLoansOrigination.png)

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/63.FabricAppsLoansOriginationImported.png)

5. Click the Integration tab and verify there’s a service called `CreditBureauMock1(1.0)`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/64.FabricAppsLoansOriginationImportedCreditB.png)

6. Click the Objects tab and verify there’s a service called `LoansApplicationObjS`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/65.FabricAppsLoansApplicationObjS.png)

7. Click the Rules tab and verify there’s a service called `LoanApprovalRules(1.0).

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/66.FabricAppsRules.png)

**Create a Workflow**

1. From your Fabric application go to the Workflow tab and click on the CONFIGURE NEW button.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/67.FabricAppsConfigureNew.png)

2. Type in a name for your workflow —e.g.: `LoansApplicationWF`

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/68.FabricAppsLoansApplicationWF.png)

3. From the Linked Object dropdown select the Use Existing option. 

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/69.FabricAppsLinkedObject.png)

4. From the list of existing object services, select the `LoanApplicationObjS` object service.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/70.FabricAppsLoanApplicationObjS.png)

5. From the list of models in this object service, select the model called `ApplicationModel`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/71.ApplicationModel.png)

6. From the list of fields in this model, select the status field and click the ADD button to save.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/72.ExistingServiceStatus.png)

7. Verify that the model `ApplicationModel` appears as linked to the newly created workflow.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/73.ApplicationModel.png)

8. In the visual workflow editor, verify that a `Start` event and a `User Task` activity have been added to the workflow.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/74.StartUserTask.png)

**Add a Task to Submit an Application**

Let's create a way for an end-user (a potential borrower) to submit an application for a loan.

1. Click the `User Task` activity, click the Properties tab to the right and rename it to `Submit Application`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/75.TaskSubmitApplication.png)

**Note**: A user task is one that can later be surfaced — either through the API or a client application — for a user to interact with the workflow.

4. In the Valid state transitions field, set the value to `New,Review,Rejected,Approved`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/76.New,Review,Rejected,Approved.png)

5. Add an `End` event to the workflow and connect the `Submit Application` task to it.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/77.SubmitApplication.png)

6. Click the SAVE button from the bottom right corner of the Console.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image044.png)

**Pro Tip**: This is not really the end of the workflow. However, for a workflow to be in a consistent state, every possible flow must have an `End`. So provisionally adding an `End` event to every possible flow is just a good way to be able to save progress. We'll add more steps before the `End` node as we progress.

[Continue to Get the Loan Applicant's Score](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/Module3-CreatingAQuantumFabricWorkflow2.md)

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()