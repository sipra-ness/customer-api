# customer-api
This is POC based API which depicts the business communication happens between reseller ecommerce system and Fuank CRM salesforce system.

This API contains one resource named as customer which has 3 methods associated with it.
The consumer can either create new customers or update the existing customer or retrieve the customer info.

For the time constraint, we have created mock services for CRM system and cosmos DB system which are the target endpoints for the consumers to perform the below operations.

Main API:  Customer API
CRM Mock app: reseller-mock-sfdc-app
DB Mock app: reseller-mock-db-app

1.	To create a new customer:

The API consumer must provide the request with relevant details of a customer without having customer Id along with username and password in the POST method in Customer API.
                  {
  "personalInformation": {
    "firstName": "Ulrich",
    "lastName": "Nielsen",
    "companyName": "E-ffoc",
    "email": "ulrichN@effoc.com",
    "phone": "+494341927420"
  },
  "address": [
    {
      "street": "Steinbrueckstrasse",
      "houseNumber": 114,
      "city": "Nuremberg",
      "country": "Germany",
      "postalCode": "90408"
    }
  ]
}
	The API will get the request, create a unique customer Id and try to hit the Mock service of CRM system & DB system. Both the end system has been wrapped in try scope to maintain the consistency in keeping the customer records in both the systems.
If one system goes down, the other system will also not accept the customer info.

2.	To update the existing customer:

The API consumer will provide the request which should contain the customer Id along with other fields for a specific customer along with username and password in the PUT method in Customer API.
		{
  "customerId": "4d4de7d6-7f5e-4778-9c70-babba6c25c55",
  "personalInformation": {
    "firstName": "Ulrich",
    "lastName": "Nielsen",
    "companyName": "E-ffoc",
    "email": "ulrichN@effoc.com",
    "phone": "+494341927420"
  },
  "address": [
    {
      "street": "Steinbrueckstrasse",
      "houseNumber": 114,
      "city": "Nuremberg",
      "country": "Germany",
      "postalCode": "90408"
    }
  ]
}
Based on the Id value, the request will enter to the down system, and it will update the records. Both the end system has been wrapped in try scope to maintain the consistency in keeping the customer records in both the systems.
If one system goes down, the other system will also not accept the customer info.

3.	To retrieve the customer Info:

The API consumer will provide the query parameter which should contain the customer Id for a specific customer along with username and password in the GET method in Customer API.

It will hit to the db mock app since it contains more detailed info about each customer and retrieve the info with 200 OK response.


Munits are created for all the 3 scenarios each having one positive and negative scenario.
