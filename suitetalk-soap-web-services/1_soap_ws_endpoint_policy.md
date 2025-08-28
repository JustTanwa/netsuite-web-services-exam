# SOAP Web Services Endpoint Policy and Upgrade Process

[Netsuite Help Center Upgrading WSDL](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3418339.html)

## What is a WSDL

A WSDL provides a description of the available services, operations and messages.

## What is a WSDL version?

Each WSDL version comes with a particular endpoint naming convention, an upgraded version could provide newer services, operations or messages.

### Example of endpoint:
- https://webservices.netsuite.com/wsdl/v2025_1_0/netsuite.wsdl
- https://webservices.netsuite.com/wsdl/v2024_2_0/netsuite.wsdl

The `v2024_2_0` is the version of the WSDL, they are released twice per year just like Netsuite version upgrades. You do not need to use the same WSDL version as your Netsuite version.

## Why upgrade WSDL?

To get access to newer services, operations or message.

## What should be considered during upgrade process?

- Retest all existing workflow in case new WSDL introduce new mandatory fields or change of data type.
- If your WSDL version will not be retired and you don't need new features you might not need to upgrade


## How does end of support and retiring of WSDL version work?

- 6 latest endpoints are supported. I.e. 2025.1, 2024.2 ... 2022.2
- 8 additional endpoints are available but without support. I.e. 2022.1 ... 2018.2
- Upgrade to a newer endpoint when your WSDL is retired, or your integrations will stop working because the old endpoint will be unavailable.

## What is the impact of new Netsuite features?

- Netsuite tries to maintain backward compatibility but some custom workflows might be affected by the Netsuite account upgrade (new features are introduced)

**Tip:** Understand what sort of errors you get when you use retired endpoints, think about what happens when you get new features and certain fields or standard records are changed, what should you do?