# Search Types and Their Implications

Good summary of search at official [search](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3514306.html) page.

[Help Center topic "Search Issues and Best Practices for SOAP Web Services and SuiteScript"](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1519647409.html)

Summary:

- Records could change during pagination
- Updated record could be removed from search results
- Added records could show up in search results
- Result could be skipped if it moved (from page 2 to 1 for example) due to record update
- Further pages could contain less than page size
- If new records of the same type, matching the search criteria, are created between a search request and a searchMoreWithId request, it can cause position changes in the results and can move records on or even out of search pages. This causes missing or duplicate records on pages.

Best Practice:
- Avoid loose search criteria that returns large dataset. Make it specific as possible.
- Using within lastModifiedDate filter
- Use Advanced Searches and reference existing saved search when possible

## Basic Search

Execute a search on a record type based on search filter fields that are specific to that type. 

This is equivalent to using filtering of the record type by one of the fields on the record. In the SOAP message, you only set field criteria, you do not dictate the search return columns. See example XML.

**NOTE: If the bodyFieldsOnly preference is set to false, a basic search triggers user event scripts and workflows. To avoid triggering user event scripts and workflows while using basic search, do one of the following: Set the bodyFieldsOnly preference to true OR Set the runServerSuiteScriptAndWorkflowTriggers preference to false.**

## Joined Search

This allow you to search for a specific record using a field on the associated (linked) record as search filters. For example, searching for Employee where you want to filter by their Supervisor's email.

You can also return the associated joined list of records this way. Using a combination of joined search and the internalId list on each record, you can retrieve a list of records for an associated list of records. For example, you can retrieve a list of contacts for a specific list of customers.

See example XML.

## Advanced Search

Execute a search on a record type in which you specify search filter fields and/or search return columns or joined search columns. Using advanced search, you can also return an existing saved search.

- You can override existing saved search return columns
- Using existing saved search, criteria are add on to existing ones
- Using existing saved search allow to utilise formula filters or expressions
- Use Advanced Search if you want only a subset of the data
- Use Advanced Search if you want user controlled search criteria
- Use Advanced Search if you want complex search that is easier achieve through UI creation
- Use Advanced Search if you want to build on existing search by adding a criteria 
- Only one saved search can be referenced per call
- You cannot return saved search with summary results

See example XML.

## Sublists in searches

Keyed sublists have a line field (typically on transaction sublists). Individual lines in the list can be searched for by referencing the line value.

Also note that when searching records, by default sublists are NOT returned in the result set, which increases the search response time. However, if you want to return all sublist data in your search, set the SearchPreferences. bodyFieldsOnly preferences to FALSE in your search request.

## Preferences

The Search Page Size preference controls the number of returned search results. It applies to both synchronous and asynchronous searches. Company-wide, valid values range from 5 to 1,000. The default value is 1,000.

You can override this preference for individual searches. For individual searches, asynchronous searches have a higher maximum than the company-wide limit

[Company Preference](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3422217.html)
