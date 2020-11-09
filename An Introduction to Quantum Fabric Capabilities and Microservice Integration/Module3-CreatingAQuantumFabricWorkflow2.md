**Get the Loan Applicant's Score**

Let's query the credit score of the new potential borrower from a credit scoring bureau. For the sake of simplicity we will mock a credit scoring service using Fabric’s Mock Service Adapter.

1. Add a `Service Task` and place it just before the `End` event — you will have to disconnect the flow arrow from `Submit Application` task and add two new ones.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image049.png)

2. Open the properties tab to the right and name the new task `Get Credit Score`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image051.png)

3.	Select `Integration Service` as the Service Type.

4.	Select `CreditBureauMock` as the service linked.

5.	Select `getScore` as the operation.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image053.png)

6. Click to configure the Input Parameters, select the credit bureau's `id_number` input parameter and map it to the model's `idDoc` field from the `BACKEND_RESPONSE` namespace.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image055.png)

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image057.png)

- **Note**: The `BACKEND_RESPONSE` namespace represents the Model on which this workflow is based —i.e. in this case the `ApplicationModel` in the `LoanApplicationObjS` service.

7. Click to configure the Output Parameters, and type in `credit` as the namespace to store the output of this service. Click the SAVE button in the modal.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image059.png)

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image061.png)

- Note: This means that if, for example, this service responds with `{"id": 1, "score": 725}`, we can later refer to `FABRIC_WORKFLOW_CONTEXT.redit.score` and the result will be the value `725`.

**Update the Loan Application**

Now let's update the loan application with the score we got from the credit bureau.

1. Again, add a `Service Task` and place it just before the `End` event. Reconnect the flow arrows accordingly.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image063.png)

2. Open the properties tab to the right and name it `Update Application`.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image065.png)

3.	Select `Object Service` as the Service Type.

4.	Select `LoanApplicationObjS` as the service linked.

5.	Select `PUT (Update)` as the operation.

6.	Click to configure the Input Parameters.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image067.png)

7.	Map `id` from the `BACKEND_RESPONSE` namespace to the id field in the model.

8.	Map `credit.score` from the `FABRIC_WORKFLOW_CONTEXT` to the `score` field in the model.

9.	Click the SAVE button in the modal and then click the SAVE button in the bottom right corner of the Console.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image069.png)

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image071.png)

**Test Our Progress So Far (Optional)**

Let's just see how we're doing. We'll publish this to an actual environment and run it there.

1. From the Fabric application click the "Publish" tab at the top.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image072.png)

2. Click the checkbox next to an environment and click the PUBLISH button in the bottom right corner. Wait until the Console shows the status is Published. You will see the application's primary and secondary app keys and secrets listed below.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image074.png)

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image076.png)

3. Click the Workflow icon just below the name of the environment. This will open a new tab to the Fabric Runtime's Console in the Workflow Services section and list the workflows published. You should see `LoansApplicationWF` in the list.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image078.png)
![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image080.png)

4. Click `LoansApplicationWF`. This will list all the instances of the `ApplicationModel` which have been pushed through the workflow. Each row shows the primary key of the model, its status, duration and relevant timestamps. Let's fire a new one.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image082.png)

5. Click the Object Services option from the main menu to the left side. This will show all the object services published. You should see the `LoanApplicationObjS` service.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image084.png)

6. Click the dropdown under the App Data Model Objects column in the `LoanApplicationObjS` row and select the `ApplicationModel`. This will display Request Input and Request Output tabs.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image086.png)

7. In the Request Input tab, select the create operation from the dropdown. This will invoke an `HTTP POST` request, so you will need a payload. Paste this in the Body of the request:

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image088.png)

```
{
{
	"idDoc": "123-1234-002",
	"status":"New",
	"firstName": "[your name]",
	"lastName": "[your last name]",
	"email": "[an email address for testing]"
}
}
```

**Note**: The `idDoc` property is meant to be used to provide whatever alphanumeric national identification or fiscal identification number is relevant to Credit Scoring in each country —e.g.: The US’s SSN, Spain’s DNI and others like these.

8. Click the Get Response button. This will switch to the Response Output and once the request succeeds it should show the following response:

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image090.png)

**Note**: The id property returned is auto-generated by the model. Take note of this value for the following steps.

9. Switch back to the Request Input and this time around select the get operation —which will fire an `HTTP GET` request— and again click the Get Response button. This time around the response should include a `records` property containing an array of all the existing loan applications.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image092.png)

10. Scroll down the body of the `records` array to the application for which the `id` matches the one in the response of the previous step. Notice that a new `score` property has been automatically added as a result of the workflow we've so far created.

![image](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/assets/image094.png)

**Pro Tip**: It's a good practice to build workflows by progressively adding and testing one or two tasks at the time. While this will require adding the `End` event in some provisional places and publishing each iteration, it is much more practical to use this approach than to try to build entire workflows all at once —especially large and complex ones.

[Continue to Assess the Score and Update the Loan Application](https://github.com/temenos/SCALE2020/blob/main/An%20Introduction%20to%20Quantum%20Fabric%20Capabilities%20and%20Microservice%20Integration/Module3-CreatingAQuantumFabricWorkflow3.md)

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()