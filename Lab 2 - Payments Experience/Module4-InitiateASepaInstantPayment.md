Module 4: Initiate a SEPA Instant payment

Purpose:	This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:

•	Initiate a SEPA instant payment transaction
•	Use modified Payment API to return transparency check response
	
Tasks:	Tasks you will complete in this lab exercise include:

•	Initiate SEPA instant payment transactions
•	Check transparency details


Step	Action
1	SEPA Instant transaction
a.	To initiate a SEPA instant transaction, we are going to use https://api.temenos.com/api/v1.0.0/order/paymentOrders/sepaInstantTransfer
b.	API documentation - https://apidocs.temenos.com/service/payment-orders#operation/createSepaInstantPayment
c.	To post a payment, we will have to form the Payload. SEPA instant payment can accept various parameters in Payload Body. 
d.	Parameters that can be used for initiating SEPA instant payment 
 


2	Initiating SEPA instant transaction
a.	In this example we will use the following Payload to initiate SEPA payment
{
  {
      "header": {},
  "body": {
    "debitAccountIBAN": "GB38DEMO60161300011215",
    "paymentCurrencyId": "EUR",
    "amount": "50",
    "beneficiaryIBAN": "GB04BARC20474473160944",
    "beneficiaryName": "Steve",
    "endToEndReference": "InstantPaymentTest1",
    "localInstrumentCode":"INST"
  }
}

b.	In Postman API should be set to POST mode
   

c.	Payload should be set in Body section of the API
 
d.	To retrieve transparency details, API is executed with “validate_only” option set to true. To set this, add “validate_only” option in Params and set the value as “TRUE”
 


e.	Execute the API by clicking Send
 
 
f.	If transparency values are accepted then the payment can be executed using the API endpoint https://api.temenos.com/api/v1.0.0/order/paymentOrders
g.	The payment Order ID returned in the previous step is used to execute the payment. PaymentOrder ID is added in the API url. This is a PUT request.
 
h.	The same payload with transparency is used in Body of this API

   {
       "header":{},
    "body": {
        "paymentCurrencyId": "EUR",
        "paymentScheme": "sepa-instant-payment",
        "amount": 50,
        "charges": [
            {
                "chargeType": "TRANSACTIONFEE",
                "chargeCurrency": "GBP",
                "chargeAmount": 5
            }
        ],
        "debitAccountIBAN": "GB38DEMO60161300011215",
        "beneficiaryName": "Steve",
        "endToEndReference": "SepaInstantPayment1",
        "beneficiaryIBAN": "GB04BARC20474473160944",
        "paymentOrderProductId": "INSTPAY-OB"
    }
   }
 


i.	Execute the API by clicking Send
 
 
 
Module 4: Lab Summary

In the fourth module, we executed an API to initiate a SEPA instant Payment, checked transparency.
