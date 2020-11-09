## Module 4: Initiate A SEPA Instant Payment

**Duration**: 30 mins

Purpose: This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:
- Initiate SEPA instant payment transactions
- Check transparency details

**SEPA Instant transaction**

1.	To initiate a SEPA instant transaction, we are going to use https://api.temenos.com/api/v1.0.0/order/paymentOrders/sepaInstantTransfer

2.	API documentation - https://apidocs.temenos.com/service/payment-orders#operation/createSepaInstantPayment

3.	To post a payment, we will have to form the Payload. SEPA instant payment can accept various parameters in Payload Body. 

4.	Parameters that can be used for initiating SEPA instant payment 

**Initiating SEPA instant transaction**

1.	In this example we will use the following Payload to initiate SEPA payment
```{
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
```
2. In Postman API should be set to POST mode
   

3. Payload should be set in Body section of the API
 
4. To retrieve transparency details, API is executed with “validate_only” option set to true. To set this, add “validate_only” option in Params and set the value as “TRUE”

5. Execute the API by clicking Send

6. If transparency values are accepted then the payment can be executed using the API endpoint https://api.temenos.com/api/v1.0.0/order/paymentOrders

7. The payment Order ID returned in the previous step is used to execute the payment. PaymentOrder ID is added in the API url. This is a PUT request.

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image027.png)

8. The same payload with transparency is used in Body of this API

```
  {
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
   ```

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image028.png)

9. Execute the API by clicking Send

![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image029.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image030.png)
![image](https://github.com/temenos/SCALE2020/blob/main/Lab%202%20-%20Payments%20Experience/images/image031.png)

**Module 4: Lab Summary**

In the fourth module, we executed an API to initiate a SEPA instant Payment, checked transparency.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()