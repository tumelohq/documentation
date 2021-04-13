# Organization Transparency

## Overview

This guide explains how to obtain a set of organizations from a set of given ISINs.

## Pre-requisites

* Must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)

### Organizations

Organizations represent public companies and other institutions such as governments that issue shares or bonds which are then traded on the world's financial markets.

## API Request Flow

### Step 1 - Authenticate

Authenticate with the Tumelo system as detailed in [Authentication](../Authentication/README.md)

### Step 2 - Listing organizations

List the organizations, queried by issued ISINs.

| Tumelo API Documentation Link | [List organizations](https://docs.tumelo.com/#operation/listOrganizations) |
|-------------------------------|---------------------------------------------------------------------------------|

## Code Example: Finding an organization that corresponds to an ISIN

In the following example, we assume you have completed the steps in the [Getting Started](../Getting_Started/README.md) guide to change your API User's temporary password and are authenticated as detailed in [Authentication](../Authentication/README.md). The following request returns the organization that has issued a particular isin of interest `GB00BKX5CN86`. 

```shell
curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/organizations?issuedIsins=GB00BKX5CN86' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

The response object may be used to outline details of the organization of interest for example with the following bits of information:

* its name
* a short bio about the company
* its logo
* a website url
* an industry classification (based off the [NAICS standard](https://www.census.gov/naics/))

```json
{
  "organizations":[
    {
      "bio":{
        "description":"Just Eat plc is a British online food order and delivery service. It acts as an intermediary between independent take-out food outlets and customers. ",
        "source":"wikipedia",
        "sourceUrl":"https://en.wikipedia.org/wiki/Just_Eat"
      },
      "displayName":"Just Eat",
      "externalIdentifiers":["LEI_213800DZ8PDXRQBBBM02"],
      "id":"ada4cdbc-c30c-411c-882f-69e60bd864d3",
      "issuedIsins": ["GB00BKX5CN86"],
      "legalName":"Just Eat PLC",
      "logoUrl":"https://res.cloudinary.com/tumelo/image/upload/w_128,h_128,c_fit/v1580302983/thoakdonplifi9uogkdz.png",
      "websiteUrl":"https://www.justeatplc.com/",
      "industry": {
        "naics2017": {
          "code": "44",
          "title": "Retail Trade"
        }
      }
    }
  ]
}
```
