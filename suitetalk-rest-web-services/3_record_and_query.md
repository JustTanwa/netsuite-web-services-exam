# Record and Query Services Implementation

Not too much note on this one, best thing I can recommend here is to just set up an integration with Postman on a sandbox or learning account and go ham exploring the REST API.

I will include some JSON examples but really this one is just about practice.

## REST API Browser

This is where you go to see the schema of records that are supported by REST Web Services, this is Netsuite's representation of the OpenAPI 3.0, which you can use swagger if you request the metadata catalogue.

## HTTP methods

CRUD operations refer is an acronym for (Create, Read, Update, Delete) and you can do all those by interacting the with REST API through the different HTTP methods.

GET - Get data
POST - Create data
PUT - Update data
DELETE - Delete data

## HATEOAS Link

Hypermedia as the engine of application state (HATEOAS) means that REST API will give you response that will contain all the information you need in order to access all the needed resource. You will see that when you request an employee there's a hyperlink that you can follow if you want to know more about subsidiary that the employee belong to. In theory, you do not need to know what endpoint to get subsidiary data, you just need to follow the link.

## Try these
- Try sending GET, POST, PUT, DELETE on a bunch of different records (standard and custom)
- Try adding, updating and deleting a sublist. E.g change item line information on a sales order
- Try interacting with subrecord. E.g add or update address of the customer
- Try transforming a record e.g. Sales Order -> Invoice
- Try Record Action if your account has any of these [Action](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1516982564.html)
- Try getting a record and use record filtering `?q` parameter to GET request
- Try using parameter like `replace` `replaceSelectedFields` to update certain fields or delete the value from the record
- Try suiteql
