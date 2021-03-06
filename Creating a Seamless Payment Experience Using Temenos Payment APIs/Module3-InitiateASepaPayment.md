## Module 3: Initiate a SEPA payment

**Duration**: 7 mins

Purpose: This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:

**Initiate a SEPA payment transaction**

**SEPA transaction**
1. To initiate a SEPA transaction, we are going to use end point https://api.temenos.com/api/v1.0.0/order/paymentOrders

2. API doc link - https://apidocs.temenos.com/service/payment-orders#operation/createPaymentOrder

3. To post a payment, we will have to form the Payload. Payment can accept various parameters in Payload Body. 

4. Parameters that can be used for initiating a payment 

![image](images/image011.png)
![image](images/image012.png)
![image](images/image013.png)
![image](images/image014.png)
![image](images/image015.png)

**Initiating SEPA transaction**
1. In this example we will use the following Payload to initiate SEPA payment
```
{
  "header": {},
  "body": {
      "paymentOrderProductId": "SEPA",
    "debitAccountIBAN": "GB88DEMO60161300080737",
    "paymentCurrencyId": "EUR",
    "amount": "50",
    "accountWithBankBIC": "BARCGB22",
    "beneficiaryIBAN": "DE92100400000012345678",
    "orderingCustomerName": "Rolf Gerling",
    "endToEndReference": "TEST SEPA",
    "executionDate": "2020-04-17",
    "beneficiaryName": "GENERAL MOTORS"
  }
}
```

2. In Postman API should be set to POST mode

![image](images/image016.png)

3. Payload should be set in Body section of the API, in RAW JSON format.  

![image](images/image017.png)

4. Execute the API by clicking Send, if Successful a transaction Status would be Success and a Payment Reference would be returned

![image](images/image018.png)
![image](images/image019.png)
![image](images/image020.png)

**Module 3: Lab Summary**

In the third module, we executed an API to initiate a SEPA Payment.

At this point, we will move on to [the fourth and final module](https://github.com/temenos/SCALE2020/blob/main/Creating%20a%20Seamless%20Payment%20Experience%20Using%20Temenos%20Payment%20APIs/Module4-InitiateASepaInstantPayment.md), where we will see how to initiate a SEPA instant payment.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey](https://forms.office.com/Pages/ResponsePage.aspx?id=D1TS1Qr2rUWGqeLnku5maQm4GcDXBTFLrQ1exd1wB_1UOTY4SFZISzRLQjU4QVVRSjlUSzExRk1CNi4u)

Get Involved in the Temenos Developer Community at [Base Camp](https://basecamp.temenos.com/s/base-camp-welcome)