# Performance Enhancement Strategies

- Use Asynchronous request for long-running requests and processing does not need to be real time
- Use SuiteQL instead of GET request on individual records when query condition gets complex
- Record filtering and query supports body fields and returns non-expanded references
- Use SuiteQL if join is necessary instead of expandSubResources
- Use PUT method to upsert record when possible
- Use APM to monitor REST Web Services
- Implement retry logic in your code

## Metadata Catalogue

Netsuite Metadata provides more data about other data, for example the meta catalogue can be used to describe the available records in Netsuite and their structure and field properties. In REST, the meta catalogue serves as the schema for what is available and it follows the OpenAPI 3.0 standard which you can copy and display on Swagger.

Therefore, it can be beneficial to refer to the metadata catalogue when forming the JSON message for unfamiliar record.
