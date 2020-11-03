## Module One: Get all payment details

**Duration**: 30 mins

At the end of this lab you should be able to:
- Get details of all the payments executed 

**Generating an API Key**
1. An API Key is required to work with API’s available in https://apidocs.temenos.com/

2. API Key can be generated in the link https://basecamp.temenos.com/s/

3. Create a login in https://basecamp.temenos.com/s/

4. Once logged in click Getting Started with Temenos APIs 

5. Click Request Key link, once done you should receive the key in email.

**Retrieving Payment Orders**

1. To retrieve executed Payment, we are going to use the API getPaymentOrders

2. API doc link - https://apidocs.temenos.com/service/payment-orders#operation/getPaymentOrders

3. Query Parameters – Following are the query parameters with which this API can be executed

**Executing API in postman**

1. API link - https://api.temenos.com/api/v1.0.0/order/paymentOrders

2. In Postman click on APIs and then open a new tab on the right side

3. Specify the API link in postman 
 
4. Generated API Key in the previous step should be added in the Header
 
5. If API executed without API key, you will receive a ‘failedToResolveAPIKey’ error.
 
6. Click ‘Send’ in Postman to execute the API.

7. If executed successfully, Status will be 200 OK and the all Payment details will be available in body. 

**Module 1: Lab Summary**

In the first module, we executed an API to extract all the payment details

At this point, we will move on to [Part 2](xx), where we will use the same API with query parameters to extract payment details of specific Ordering Customer.

**Rate Temenos SCALE**

Let us know how we did via our [Feedback Survey]()