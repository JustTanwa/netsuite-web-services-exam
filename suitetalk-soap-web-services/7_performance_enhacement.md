# Performance Enhancement Strategies

[Official Doc](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1537861842.html)

- Use Web Services Only Forms
- Using existing saved search with advanced search
- Use context API for user event script
- Disable script and workflow for historical imports
- Use list operations when possible (addList...), can add multiple record types in one request
- Use Asynchronous whenever possible
- Use TBA to avoid concurrency issues
- Disable system notes for custom fields, log system note on update only (request-level preference and general preference respectively)
- Use APM to monitor and analyse performance
- Use upsertList over addList (this will create record if not exist, however needs externalid so only works on record that supports this) to avoid duplicates and save on addList/updateList.