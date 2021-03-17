# Organization Transparency

## Overview

This guide explains how to obtain a set of organizations from a set of given ISINs.

## Pre-requisites

* Must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)

### Organizations

Organizations represent public companies and other institutions such as governments that issue shares or bonds which are then traded on the world's financial markets.

## API Request Flow

### Step 1 - Authenticate

Authenticate with the Tumelo system

### Step 2 - Listing organizations

List the organizations, queried by issued ISINs.

| Tumelo API Documentation Link | [List organizations](https://docs.tumelo.com/#operation/listOrganizations) |
|-------------------------------|---------------------------------------------------------------------------------|

## Code Example

In the following example, we assume you have completed the steps in the [Getting Started](../Getting_Started/README.md) guide to change your API User's temporary password. The example illustrates how to obtain an authentication from the Tumelo API, however in practice we recommend the use of one of the Cognito client libraries which make obtaining and refreshing tokens straightforward. For further details see the [Authentication](../Authentication/README.md) guide.

#### cURL

Getting the ID token (step 1).

```shell
ID_TOKEN=$(curl --location -s --request POST 'https://api.prod.tumelo.com/v1/authenticate' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
        "habitatId": "{HABITAT_ID}",
        "username": "{USERNAME}",
        "password": "{PASSWORD}"
}' | jq -r '.token')
```

Listing organizations (step 2).

```shell
curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/organizations?issuedIsins=GB00BKX5CN86' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

## Example Response

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
      "websiteUrl":"https://www.justeatplc.com/"
    }
  ]
}
```