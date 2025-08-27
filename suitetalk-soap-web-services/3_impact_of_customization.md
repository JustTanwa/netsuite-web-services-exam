# Impact of Customizations on SOAP Web Services

It is possible to customise Netsuite with custom objects such as custom fields, custom record, custom segments and custom forms. These can have impact on your SOAP Web Services.

It is recommend that you have SOAP specific form so that you do not run into required fields or hidden fields error if you customize a specific form for a set of users. This can be done when editting the custom form to have "web-services-specific" setting.

- Have SOAP Web Services specific form
- Custom display only (inline) and disabled fields are not settable through SOAP web services because these are NOT settable through the UI. If you provide a value in your SOAP web services request for such a field, an error message is returned.
- Hidden fields are not readable in SOAP web services
- The bodyFieldsOnly request-level preference affects the way formulas on forms are processed. As a result, if the values of custom fields are calculated using formulas, the search might return incorrect results. If the calculated values of formulas are incorrect, set the bodyFieldsOnly preference to false to make sure the correct values are returned. 
- Request-level **override** company-wide settings.

## Available Request-Level Preferences
- disableMandatoryCustomFieldValidation
- disableSystemNotesForCustomFields (can improve performance)
- ignoreReadOnlyFields (can result in INSUFFICIENT_PERMISSION if false)
- runServerSuiteScriptAndWorkflowTriggers (good to turn off for historical imports)
- warningAsError
- bodyFieldsOnly (search result to ignore sublists, default is true for basic search)
- pageSize (5-1000 for Synchronous, 5- 2000 for Async)
- returnSearchColumns

## Custom Record

RecordRef and CustomRecordRef are descend of BaseRef so they have a type attribute. 

Understanding if Custom Record have Name field, or some sort of auto generated numbering.

- The Auto box is labeled autoName in SOAP web services.
- The ID field is labeled name in SOAP web services. This field is read only if the autoName value is true.
 -The Name field is labeled altName in SOAP web services.