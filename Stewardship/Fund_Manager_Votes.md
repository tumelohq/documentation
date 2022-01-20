# Fund Manager Votes and Significant Votes

## Overview

This guide explains how to obtain the voting information for a given fund manager. Tumelo collects fund manager voting information, including those votes the fund manager has identified as [significant](#definitions) on a regular basis, direct from the fund managers. The frequency with which voting information is updated varies between fund managers, but most provide updates at least once every three months. Please contact your Tumelo account manager of you require further information.

### Subscribed instruments

When you set up access to Tumelo's API, you tell us which funds you would like to be able to get fund manager voting information for. We refer to these as your [Subscribed Instruments](https://docs.tumelo.com/#section/Subscribed-Instruments). 

If you are not seeing voting information for funds you would expect to see, please check the fund in question appears in your habitat's subscribed instrument list in the first instance. If you believe your subscribed instrument list is complete and the expected information is still not available, please contact [Tumelo Support](mailto:support@tumelo.com) for further advice.

If you would like to change your subscribed instrument list, please contact your Tumelo account manager.

## Prerequisites

* Must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)
* Your habitat must be subscribed to one or more composite instruments. _The fund manager information and voting information that is available to you will depend on the composite instruments your habitat is subscribed to_. 

## Definitions

* **Significant vote** - a significant vote is a vote that the fund manager has identified as significant on their [PLSA](https://www.plsa.co.uk) template. See the PLSA's voting template [implementation guidance](https://www.plsa.co.uk/Policy-and-Research/Document-library/Implementation-Statement-guidance-for-trustees) for further information.

## API Request Flow

### Step 1 - Authenticate

Authenticate with the Tumelo system.

### Step 2 - Check your Subscribed Instrument List

List the instruments in your habitat that are available for requesting fund manager voting information on. Fund manager voting information is only associated with composite instruments (also referred to as "funds"). Non-composite instruments do not have any fund manager voting information associated with them.

| Tumelo API Documentation Link | [List subscribed instruments](https://docs.tumelo.com/#section/Subscribed-Instruments) |
|-------------------------------|----------------------------------------------------------------------------------------|

### Step 3 - Listing Fund Managers

In order to obtain the list of the fund managers for which voting information is available to you, based on your subscribed instrument list, and to discover the relevant fund manger ID to use in subsequent steps.

| Tumelo API Documentation Link | [List fund managers](https://docs.tumelo.com/#operation/listFundManagers) |
|-------------------------------|----------------------------------------------------------------------------------------|

### Step 4 - Listing Managed Instruments for a Fund Manager

Using the ID of one of the fund managers returned in the previous step, you can verify the list of the instruments managed by the given fund manager that are available for requesting voting information for.

| Tumelo API Documentation Link | [List managed instruments](https://docs.tumelo.com/#operation/listManagedInstruments) |
|-------------------------------|----------------------------------------------------------------------------------------|

### Step 5 - Listing Fund Manager Votes or Significant Votes for a Managed Instrument

Having obtained the relevant fund manager ID and confirmed the required instrument is included in the managed instrument list for the fund manager, you can request the list of votes or significant votes that were cast by the fund manager for the instrument.

| Tumelo API Documentation Links | [List fund manager votes](https://docs.tumelo.com/#operation/listFundManagerVotes) and [List fund manager significant votes](https://docs.tumelo.com/#operation/listFundManagerSignificantVotes) |
|-------------------------------| -------------------------------------------------------------------------|

## Sequence Diagram

[![](https://mermaid.ink/img/eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQVBJIFVzZXItPj4rVHVtZWxvIEFQSTogQWNxdWlyZSBBY2Nlc3MgVG9rZW5cbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogUG9zdCAvdjEvYXV0aGVudGljYXRlXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IEFjY2VzcyBUb2tlblxuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBHZXQgL3YxL2hhYml0YXRzL3toYWJpdGF0SWR9L2luc3RydW1lbnRzXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IExpc3Qgb2YgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgRnVuZCBNYW5hZ2Vyc1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBHZXQgL3YxL2Z1bmRNYW5hZ2Vyc1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IG9mIEZ1bmQgTWFuYWdlcnNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBMaXN0IE1hbmFnZWQgSW5zdHJ1bWVudHNcbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogR2V0IC92MS9mdW5kTWFuYWdlcnMve2Z1bmRNYW5hZ2VySWR9L21hbmFnZWRJbnN0cnVtZW50c1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IG9mIE1hbmFnZWQgSW5zdHJ1bWVudHNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBSZXF1ZXN0IFZvdGVzIGZvciBNYW5hZ2VkIEluc3RydW1lbnRcbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogR2V0IC92MS9mdW5kTWFuYWdlcnMve2Z1bmRNYW5hZ2VySWR9L21hbmFnZWRJbnN0cnVtZW50cy97aXNpbn0vdm90ZXNcbiAgICBUdW1lbG8gQVBJLS0-Pi1BUEkgVXNlcjogVm90ZXMgZm9yIE1hbmFnZWQgSW5zdHJ1bWVudCIsIm1lcm1haWQiOnsidGhlbWUiOiJiYXNlIiwic2VxdWVuY2UiOnsibWlycm9yQWN0b3JzIjpmYWxzZSwic2hvd1NlcXVlbmNlTnVtYmVycyI6ZmFsc2V9fSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid-js.github.io/mermaid-live-editor/edit#eyJjb2RlIjoic2VxdWVuY2VEaWFncmFtXG4gICAgQVBJIFVzZXItPj4rVHVtZWxvIEFQSTogQWNxdWlyZSBBY2Nlc3MgVG9rZW5cbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogUG9zdCAvdjEvYXV0aGVudGljYXRlXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IEFjY2VzcyBUb2tlblxuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBHZXQgL3YxL2hhYml0YXRzL3toYWJpdGF0SWR9L2luc3RydW1lbnRzXG4gICAgVHVtZWxvIEFQSS0tPj4tQVBJIFVzZXI6IExpc3Qgb2YgU3Vic2NyaWJlZCBJbnN0cnVtZW50c1xuICAgIEFQSSBVc2VyLT4-K1R1bWVsbyBBUEk6IExpc3QgRnVuZCBNYW5hZ2Vyc1xuICAgIE5vdGUgb3ZlciBBUEkgVXNlcixUdW1lbG8gQVBJOiBHZXQgL3YxL2Z1bmRNYW5hZ2Vyc1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IG9mIEZ1bmQgTWFuYWdlcnNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBMaXN0IE1hbmFnZWQgSW5zdHJ1bWVudHNcbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogR2V0IC92MS9mdW5kTWFuYWdlcnMve2Z1bmRNYW5hZ2VySWR9L21hbmFnZWRJbnN0cnVtZW50c1xuICAgIFR1bWVsbyBBUEktLT4-LUFQSSBVc2VyOiBMaXN0IG9mIE1hbmFnZWQgSW5zdHJ1bWVudHNcbiAgICBBUEkgVXNlci0-PitUdW1lbG8gQVBJOiBSZXF1ZXN0IFZvdGVzIGZvciBNYW5hZ2VkIEluc3RydW1lbnRcbiAgICBOb3RlIG92ZXIgQVBJIFVzZXIsVHVtZWxvIEFQSTogR2V0IC92MS9mdW5kTWFuYWdlcnMve2Z1bmRNYW5hZ2VySWR9L21hbmFnZWRJbnN0cnVtZW50cy97aXNpbn0vdm90ZXNcbiAgICBUdW1lbG8gQVBJLS0-Pi1BUEkgVXNlcjogVm90ZXMgZm9yIE1hbmFnZWQgSW5zdHJ1bWVudCIsIm1lcm1haWQiOiJ7XG4gIFwidGhlbWVcIjogXCJiYXNlXCIsXG4gIFwic2VxdWVuY2VcIjoge1xuICAgICAgXCJtaXJyb3JBY3RvcnNcIjogZmFsc2UsXG4gICAgICBcInNob3dTZXF1ZW5jZU51bWJlcnNcIjogZmFsc2VcbiAgfVxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)

## Code example

## Code Example

The following code snippets walk you through the sequence of calls described above using a command line client and cURL.

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

Listing your subscribed instruments (step 2).

```shell
export HABITAT_ID={your habitat here}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/instruments' \
    --header 'Authorization: Bearer '$ID_TOKEN
```
Listing your fund managers (step 3)

```shell
curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/fundManagers' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

Listing the instruments managed by a given fund manager (step 4)
```shell
export FUND_MANAGER_ID={your selected fund manager ID}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/fundManagers/'$FUND_MANAGER_ID'/managedInstruments' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

Listing the votes for your chosen instrument (step 5)
```shell
export ISIN={ISIN of your chosen fund}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/fundManagers/'$FUND_MANAGER_ID'/managedInstruments/'$ISIN'/votes' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

## Example Vote Response

```json
{
    "fundManagerVotes": [
        {
            "fundManagerId": "d2dbc903-44e7-43a8-b8e2-c010a31716bc",
            "generalMeetingId": "478484d8-9cdf-4554-a954-daa0f3d1832d",
            "id": "f2ab0034-77ae-4317-950d-980d5746c309",
            "instruction": "against",
            "isins": [
                "GB00B6V6WH96"
            ],
            "organizationId": "58383760-0c89-4c3f-b278-de76dcfa0a01",
            "proposalId": "4cb1f111-3546-4fb4-b467-f1b3f8d9eb0f",
            "rationale": "Joint Chair/CEO: A vote against is applied as LGIM expects companies to separate the roles of Chair and CEO due to risk management and oversight.Board mandates: A vote against is applied as LGIM expects a CEO or Non-Executive Directors not to hold too many external roles to ensure they can undertake their duties effectively."
        },
        {
            "fundManagerId": "d2dbc903-44e7-43a8-b8e2-c010a31716bc",
            "generalMeetingId": "453da2c4-9b70-4cef-912b-4e33efcbc9d3",
            "id": "a9be099a-0faa-49fb-b705-20a756d313dc",
            "instruction": "for",
            "isins": [
                "GB00B6V6WH96"
            ],
            "organizationId": "6a2e39da-4ac0-4121-8188-6fdddcd7a025",
            "proposalId": "965fd933-1bcf-4a3f-bf69-3cada5c69993",
            "rationale": "A vote FOR this proposal is warranted given that elimination of the supermajority vote requirement would enhance shareholder rights."
        }
    ],
    "nextPageToken": ""
}
```


Listing the significant votes for your chosen instrument (step 5)
```shell
export ISIN={ISIN of your chosen fund}

curl --location --request \
	GET 'https://api.prod.tumelo.com/v1/fundManagers/'$FUND_MANAGER_ID'/managedInstruments/'$ISIN'/significantVotes' \
    --header 'Authorization: Bearer '$ID_TOKEN
```

## Example Significant Vote Response

```json
{
    "fundManagerSignificantVotes": [
        {
            "fundManagerId": "d2dbc903-44e7-43a8-b8e2-c010a31716bc",
            "generalMeetingId": "f214b9cb-4e35-4b81-8ae1-9539edec295e",
            "id": "d97ff3cb-2e44-4255-a17a-3dd3d07ed3fe",
            "isins": [
                "GB00B6V6WH96"
            ],
            "organizationId": "ecf0a507-bcad-4c83-afed-6d87363883b0",
            "proposalId": "c658ed3b-60fd-484f-8f4f-92b744ef5b8b",
            "rationale": "Since the beginning of the year there has been significant client interest in our voting intentions and engagement activities in relation to the 2020 Barclays AGM. We thank our clients for their patience and understanding while we undertook sensitive discussions and negotiations in private. We consider the outcome to be extremely positive for all parties: Barclays, ShareAction and long-term asset owners such as our clients."
        }
    ],
    "nextPageToken": ""
}
```