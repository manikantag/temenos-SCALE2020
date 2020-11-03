Module 3: Initiate a SEPA payment

Purpose:	This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:

•	Initiate a SEPA payment transaction
	
Tasks:	Tasks you will complete in this lab exercise include:

•	Initiate payment transactions
 
Step	Action
1	SEPA transaction
a.	To initiate a SEPA transaction, we are going to use end point https://api.temenos.com/api/v1.0.0/order/paymentOrders
b.	API documentation - https://apidocs.temenos.com/service/payment-orders#operation/createPaymentOrder
c.	To post a payment, we will have to form the Payload. Payment can accept various parameters in Payload Body. 
d.	Parameters that can be used for initiating a payment 

2	Initiating SEPA transaction
a.	In this example we will use the following Payload to initiate SEPA payment
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

a.	 In Postman API should be set to POST mode
b.	Payload should be set in Body section of the API
 
c.	Execute the API by clicking Send, if Successful a transaction Status would be Success and a Payment Reference would be returned
	
Module 3: Lab Summary

In the third module, we executed an API to initiate a SEPA Payment.

At this point, we will move on to Part 4. Where we will see how to initiate a SEPA instant payment.
