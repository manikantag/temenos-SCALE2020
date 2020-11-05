## Module 3: Initiate a SEPA payment

**Duration**: 30 mins

Purpose: This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:

**Initiate a SEPA payment transaction**

**SEPA transaction**
1. To initiate a SEPA transaction, we are going to use end point https://api.temenos.com/api/v1.0.0/order/paymentOrders
2. API documentation - https://apidocs.temenos.com/service/payment-orders#operation/createPaymentOrder
3. To post a payment, we will have to form the Payload. Payment can accept various parameters in Payload Body. 
4. Parameters that can be used for initiating a payment 

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image011.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image012.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image013.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image014.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image015.png)

**Initiating SEPA transaction**
1. In this example we will use the following Payload to initiate SEPA payment
```
{
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

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image016.png)

3. Payload should be set in Body section of the API

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image017.png)

4. Execute the API by clicking Send, if Successful a transaction Status would be Success and a Payment Reference would be returned

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image018.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image019.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image020.png)

**Module 3: Lab Summary**

In the third module, we executed an API to initiate a SEPA Payment.

At this point, we will move on to [Part 4](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/Module4-InitiateASepaInstantPayment.md), where we will see how to initiate a SEPA instant payment.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()