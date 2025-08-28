# Record and Sublist Interactions

## Stand Records

Most standard Netsuite records are supported by the SOAP WS. For full list, check the help center.

For SOAP API, the Record is a main reference for all record type, and all other supported records are sub-class or a type of Record.

The three broad categories of records are:
- Record Types (Customer, Sales Order ...)
- Search Records (Represents a Saved Search for a particular record type e.g. Transaction)
- Subrecords (addresses, inventory details...)

## Fields and Custom Fields

Within a record there will be standard fields and custom fields. In SOAP, a field is typically referred to by the tag name and it's important to determine the correct field type. You may need to look into how to populate different field types, for example how should a date field be populated, what about an ENUM field like transaction type?

### Field Types:
- String
- Int
- Double
- RecordRef (Select field or drop down fields)
- Enum
- List

Standard fields are included in all Netsuite accounts.

Custom Fields are created to customise an account through SuiteBuilder. Custom fields are always listed under the `customFieldList` XML element. See XML stub examples I have prepared.

- Beware of mandatory fields, this will throw an error if XML message is missing those values
- Customization made to standard fields are respected in SOAP WS, if it is disabled or not shown on a form, it cannot be set via SOAP.
- get operation does not return custom hidden fields.
- Hidden fields are not readable in SOAP except for `lastModifiedDate`, `createdDate`, `created`, `lastModified`, and `externalID`  
- bodyFieldsOnly preference affects calculated formula fields.

## Sublist

Sublist are the table or list you see on standard (or custom) records, for example item sublist on Sales Order. You will need to understand how to interact with these when creating and updating records that supports sublists.

Record element (XML element) that ends with  **List** is a hint that it is a sublist, with the exception for `customFieldList` which is a list of custom fields.

**Custom sublists are not available in SOAP web services.**


### Keyed and Non-Keyed sublists

#### Keyed Sublist

Indexing line element or internal ID can be used as the key to update the line, this allow you to use `replaceAll` attribute to update only specific lines, this value needs to be set to `false`. If `replaceAll` is `true`, all existing lines on the record not match to XML lines will be removed, matching lines will be updated and lines in XML without matching record lines will be added.

#### Non-Keyed Sublist

The sublist which have no indexing line element or internal ID that can be used as a key. It is considered to be a flat list. Because of this nature you should always update every single line even if you want to update one, this is because `replaceAll` is ignored.

- To update a single line in the sublist, retrieve the entire sublist, change a single line as desired, and then resubmit the entire sublist.
- To replace the sublist with a subset of lines, retrieve the entire sublist, and then resubmit the subset of lines. The original sublist is purged and replaced by the new sublist containing the subset of lines.
- To delete the sublist, submit an empty sublist. See Deleting All Lines on a Sublist for more information.

## Subrecords 

Subrecords are much like standard records but only caveat is that you can only interact with it through a parent record and cannot access the subrecord and update that alone. [Subrecords](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3432503.html)

- `replaceAll` attribute also control whether all subrecord is overwritten or not.

## getCustomizationId oepration

A SOAP operation that will list all the custom objects within a Netsuite account, custom records, fields, lists etc. [Detailed explanataion and examples](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N3493817.html)

- Use this method to get list of objects, then chain a get or getList request to get more object metadata (field type etc...)
- Identifier of the customisation are in this order: internalId, externalId, scriptId. This mean if one of the first two is correct, scriptId can be invalid.

## Schema Browser

A place to see all the record and their field definitions, you can see which fields are required for each record type. 

They are also versioned according to Netsuite version, because fields can be added or removed so pay attention to version. [2024_1 Schema Browser](https://system.netsuite.com/help/helpcenter/en_US/srbrowser/Browser2024_1/script/record/account.html)

