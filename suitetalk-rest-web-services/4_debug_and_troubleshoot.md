# Debugging and Troubleshooting

REST Web Services share concurrency with SOAP and Restlet so it is possible to reach concurrency limit when there are a lot of integrations. 

REST Response will contain HTTP status code which will inform you about the success or failure of the request. You can review the `o:errorDetails` property for the details of the error. For example, when a request exceeds the concurrency limit you will get example response:

```
{
  "type": "https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html",
  "title": "Bad Request",
  "status": 429,
  "o:errorCode": "USER_ERROR"
  "o:errorDetails": [
    {
      "detail": "Concurrent request limit exceeded. Request blocked.",
      "o:errorCode": "CONCURRENCY_LIMIT_EXCEEDED"
    }
  ]
} 
```

For errors with the status code of `5XX` that is related to the server internal error and a contact to Netsuite Customer Support is needed.

The typical HTTP status codes are:
- 2XX: Successful request
- 4XX: Failure due to user error
- 5XX: Failure due to system error

## Login Audit Trail

If you get "Unauthorized" error code you can review the Login Audit Trail for more details about why the request was rejected.

## Integration Record

The integration record will show the history REST Web Services execution log, there you can view the previous request and response JSON.

## Limitations

Understanding limitations can help with debugging and troubleshooting when things don't work out as you through.

[Limitataion of REST](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/chapter_1540391670.html#subsect_1559222360)
