# Instrument breakdown of an instrument

## Overview

This guide explains how to obtain an instrument breakdown of a fund or other *composite instrument* in order to provide detailed information about the exposure to the instruments residing in that root instrument. For an overview of instrument breakdowns, see the [What is Transparency](../What_is_Transparency/README.md) guide.

The composite instrument's instrument breakdown allows you to know exactly how the instrument's own investments are distributed across underlying instruments. 

In order to get an instrument breakdown on a specific composite instrument, your company must have included the instrument in your subscribed instruments list. To update subscribed instruments, get in touch with us at [support@tumelo.com](mailto:support@tumelo.com).

## Pre-requisites

* Must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)
* Your habitat must be subscribed to one or more composite instruments

## Definitions

* **Composite instrument**: A composite instrument will be invested into other instruments, such as shares, bonds or even other composite instruments. There are many types of composite instruments (mutual, OEIC, ETFs, etc…) but all have this basic structure.

### Subscribed instruments

When you set up access to Tumelo's API, you tell us which funds you would like to be able to get instrument breakdowns for (see Getting Started). We refer to these as your [Subscribed Instruments](https://docs.tumelo.com/#section/Subscribed-Instruments). You may request an organization breakdown on any composite instrument that appears in your subscribed instrument list.

## API Request Flow

### Step 1 - Authenticate

Authenticate with the Tumelo system

### Step 2 - Listing subscribed instruments

List the instruments in your habitat that are available for requesting an instrument breakdown on. This is to find the ISINs of the instruments in your subscribed instrument list and to check which of your subscribed instruments are composite.

| Tumelo API Documentation Link | [List subscribed instruments](https://docs.tumelo.com/#section/Subscribed-Instruments) |
|-------------------------------|----------------------------------------------------------------------------------------|

### Step 3 - Get Breakdown

Get the instrument breakdown for a composite instrument.

The output of this step will provide the organizations in which the composite instrument is invested. Each instrument in the breakdown is given a weighting indicating the relative investment ownership within the composite instrument. If you request an organization breakdown on a non-composite instrument from your subscribed list, the API will return an error.

| Tumelo API Documentation Link | [Get instrument breakdown for a composite instrument](https://docs.tumelo.com/#operation/getInstrumentBreakdownByIsinInHabitat) |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|

## Sequence Diagram

[![](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQVBJIFVzZXItPj4rVHVtZWxvIEFQSTogQWNxdWlyZSBBY2Nlc3MgVG9rZW5cbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogUG9zdCAvdjEvYXV0aGVudGljYXRlXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IEFjY2VzcyBUb2tlblxuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBQb3N0IC92MS9oYWJpdGF0cy97aGFiaXRhdElkfS9pbnN0cnVtZW50c1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IE9mIFN1YnNjcmliZWQgSW5zdHJ1bWVudHNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBSZXF1ZXN0IEluc3RydW1lbnQgQnJlYWtkb3duXG4gICAgTm90ZSBvdmVyIEFQSSBVc2VyLFR1bWVsbyBBUEk6IEdldCAvdjEvaGFiaXRhdHMve2hhYml0YXRJZH0vaW5zdHJ1bWVudHMve2lzaW59L2luc3RydW1lbnRCcmVha2Rvd25cbiAgICBUdW1lbG8gQVBJLS0-Pi1BUEkgVXNlcjogSW5zdHJ1bWVudCBCcmVha2Rvd25cbiIsIm1lcm1haWQiOnsidGhlbWUiOiJiYXNlIiwic2VxdWVuY2UiOnsibWlycm9yQWN0b3JzIjpmYWxzZX19LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQVBJIFVzZXItPj4rVHVtZWxvIEFQSTogQWNxdWlyZSBBY2Nlc3MgVG9rZW5cbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogUG9zdCAvdjEvYXV0aGVudGljYXRlXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IEFjY2VzcyBUb2tlblxuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBQb3N0IC92MS9oYWJpdGF0cy97aGFiaXRhdElkfS9pbnN0cnVtZW50c1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IE9mIFN1YnNjcmliZWQgSW5zdHJ1bWVudHNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBSZXF1ZXN0IEluc3RydW1lbnQgQnJlYWtkb3duXG4gICAgTm90ZSBvdmVyIEFQSSBVc2VyLFR1bWVsbyBBUEk6IEdldCAvdjEvaGFiaXRhdHMve2hhYml0YXRJZH0vaW5zdHJ1bWVudHMve2lzaW59L2luc3RydW1lbnRCcmVha2Rvd25cbiAgICBUdW1lbG8gQVBJLS0-Pi1BUEkgVXNlcjogSW5zdHJ1bWVudCBCcmVha2Rvd25cbiIsIm1lcm1haWQiOnsidGhlbWUiOiJiYXNlIiwic2VxdWVuY2UiOnsibWlycm9yQWN0b3JzIjpmYWxzZX19LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)


## Code Example

In the following example, we assume you have completed the steps in the [Getting Started](../Getting_Started/README.md) guide to change your API User's temporary password. The example illustrates how to obtain an ID token from AWS Cognito using their HTTP API in order to provide the authentication credentials required by the Tumelo API, however in practice we recommend the use of one of the Cognito client libraries which make obtaining and refreshing tokens straightforward. For further details see the [Authentication](../Authentication/README.md) guide.

#### cURL

Getting the ID token (step 1).

```shell
ID_TOKEN=$(curl --location -s --request POST 'https://api.prod.tumelo.com/v1/authenticate' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
        "username": "{USERNAME}",
        "password": "{PASSWORD}"
}' | jq -r '.token')
```

Listing your subscribed instruments (step 2).

```shell
export HABITAT_ID={your habitat here}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/instruments' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

Getting the instrument breakdown (step 3).

```shell
export HABITAT_ID={your habitat here}
export ISIN={chosen ISIN here}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/instruments/'$ISIN'/instrumentBreakdown' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

## Example Breakdown Response

```json
{
  "basedOn": {
    "instruments": [
      {
        "instrument": {
          "isin": "GB00B7VT0938"
        },
        "validAt": "2019-12-19T10:27:12.234Z"
      }
    ]
  },
  "components": {
    "cash": [
      {
        "currency": "GBP",
        "weight": 0.375
      }
    ],
    "instruments": [
      {
        "weight": 0.25,
        "instrument": {
          "isin": "US0378331005",
          "title": "APPLE INC",
          "mifirCode": "SHRS",
          "isComposite": false
        }
      },
      {
        "weight": 0.25,
        "instrument": {
          "isin": "US0231351067",
          "title": "AMAZON.COM INC",
          "mifirCode": "SHRS",
          "isComposite": false
        }
      }
    ],
    "others": 0.125
  },
  "readTime": "2020-07-23T09:45:35.311128394Z"
}
```