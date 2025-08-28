# Debugging and Troubleshooting

## Currency and Privileges

Role drives the permissions what the SOAP Web services user can do in Netsuite. You can encounter INSUFFICIENT_PERMISSION errors when the role does not have ncessary permission for the operation.

It is recommended to create custom role and custom form when building and testing the integration to avoid unforseen limitation which some times happen if SOAP is developed with Admin role. This is also in line with the rule for minimal necessary priviledges.

- Role require SOAP Web Services permission 
- Role can be set as to be Web Services Only Role to avoid users logging in via the UI
- Default Web Services role can be set under SOAP WS Peferences

Concurrecy is based on account tier and SuiteCloud Plus licenses. All integrations share the same limit, and you can encounter this error when the limit is reached: `ExceededConcurrentRequestLimitFault` or `ExceededRequestLimitFault`.

Each SC+ license adds 10 concurrencies, the number of SC+ avaialble depends on the account tier. Standard, Premium, Enterprise, Ultimate starts with 5, 15, 20, 20 respectively with each you can buy up to 1, 3, 6, 12 SC+ licenses respectively.

## Warning vs errors vs faults

[Official Docs](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3536574.html)

- Warning: Informational, in SOAP data may or may not be processed depending on preferences. 
- Errors: Exception are return record-by-record basis, this could be missing required fields or incorrect field values. Successful records are processed.
- Fault: Entire request not processed. Example, invalid login attempt due to auth issue. [Fault List](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3539420.html)

## Error handling

Within the integration, it is recommended to use a Try/Catch block inside the code to catch specific exceptions/faults to handle it to prevent breaking of the integration.

SuiteTalk errors can be found in the `statusDetail` if `isSuccess` attribute of the `status` XML element is false. You can use this information to display or log it so that it can be resolved. 

You can use Login Audit Trail with "Detail" column to debug why a SOAP request did not pass authentication. The common issues are:

- NonceUsed: Request contains same nonce and timestamp which was already processed
- InvalidTimestamp: More than 5 minutes have passed since request was generated or timestamp is different than server time
- InvalidSignature: Request was not signed correctly.

## SOAP Web Services Logs

With Netsuite UI, you can view the SOAP Web Services Usage Log under integration for details on the request received and response sent. **Only Admin** can access this page.

- Logs last for 21 days (can be earlier if heavy usage)
- Request larger than 100MB is not logged
- Response larger than 10MB is not logged

The above page is for debugging synchronous SOAP requests only.

For Asynchronous SOAP Request users can view Setup > Integration > SOAP Web Services Process Status, if they have at least VIEW SOAP Web Services Logs permission or FULL SOAP Web Services permission. Similar limitation for saved request and response as above. On this page you can track job which are in progress and view details of those that have completed successfully. 

**Tip:** There is a search type called Soap Web Services Logs that you can explore to see what is possible to be reported there and how you can utilise it to debug certain requests.
