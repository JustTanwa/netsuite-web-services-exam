# Multi-Platform Concurrency Management

[Concurrency Cheatsheet](https://nlcorp.app.netsuite.com/core/media/media.nl?id=205292151&c=NLCORP&h=1a5af77f3fdd806dea9e&_xt=.pdf)

You need to understand the Netsuite Service Tier and SuiteCloud Plus license model which grant number of concurrency for the account wide based on those combination. The cheatsheet above gives really good overview of different scenarios where request might fail given certain scenarios. I highly recommend checking that out.

In general, you would not limit concurrency to a particular integration record, but if you want to control an integration so that it does not flood your account with request and blocking other integrations you can use this setting. This does mean that if the specific integration goes through peak request it can generate fail requests when a limit is in place.

Use APM to monitor the peak and average concurrency to decide if more SuiteCloud Plus license should be purchased.

Each integration should have a robust retry mechanism to and error handing when request limit is exceeded, this is to prevent loss data and cascading failures or following requests.

**Highly Recommend** Reviewing what error message you can get in both SOAP and REST when limit is exceeded, look at the Integration Governance page and play around with Concurrency Limit on integration record.
