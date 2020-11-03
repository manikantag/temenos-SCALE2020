Module 2: Get Payments based on Ordering Customer

Purpose:	This lab introduces the subject of working with Payment API’s 
After completing the lab, you should be able to:

•	Get all payments executed for a Customer
	
Tasks:	Tasks you will complete in this lab exercise include:

o	Get list of all Payments by Customer Number
 
Step	Action
1	Retrieving Payment Orders
a.	To retrieve Payments created for a customer, we are going to use the same API getPaymentOrders
b.	API doc link - https://apidocs.temenos.com/service/payment-orders#operation/getPaymentOrders
c.	Query Parameters – Following are the query parameters with which this API can be executed, we will be using the parameter ‘orderingCustomerId’
 
2	Filtering using query parameter
a.	API link - https://api.temenos.com/api/v1.0.0/order/paymentOrders
b.	Specify the API link in postman 

c.	To get list of all payments for a customer, add “?orderingCustomerId=<CustomerID>” in API link 
 
d.	Click Send to execute API, it will get all Payments for ordering customer 100343 

Module 2: Lab Summary

In the second module, we executed an API to extract all the payment details for an ordering customer.

At this point, we will move on to Part 3, we will initiate a SEPA payment transaction.
