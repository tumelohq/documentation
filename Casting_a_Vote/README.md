# Casting a Vote

## Overview

This guide explains how to use the Tumelo API to submit an investor's voting preference on a specific proposal being voted on at a company's forthcoming AGM. 

A ballot provides the means by which an investor's voting preference can be submitted to Tumelo. For an overview of ballots, proposals and polls, please see the [What is Voting](../What_is_Voting/README.md) guide.

The [Investor Ballots](../Investor_Ballots/README.md) guide explains how to discover which ballots are available to a given investor, and which of these are still available for submitting a vote preference. The same guide also shows how discover the way in which the investor voted on previous ballots.

## Pre-requisites

* You must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)
* Your habitat must be subscribed to one or more composite instruments
* You must have created one or more investors
* At least one investor must have an investor account with at least one composition record (see [Investor Account Transparency](../Investor_Account_Transparency/README.md)).
* A ballot must be available for submission

## Casting a vote

Once you have collected the voting preference on a poll for a specific investor through the user interface of your application, you should use the ballot assigned to that investor for the relevant poll to submit the investor's vote preference to Tumelo.

The [castVote](https://docs.tumelo.com/#operation/castVote) API endpoint allows you to submit the vote preference for a specific poll using the appropriate ballot entity.

Let's assume that the following response has been received from an earlier call to `listBallots` for the investor with ID `d9d72655-ffca-4548-bac3-defd131dcefe` and we now want to record a "_for_" response for the investor to poll ID `0a0b3061-200d-4b1b-82da-034189614592`. We can see that a vote preference for this ballot has not been recorded yet since it includes no `investorVote` property.

```json
{
    "ballots": [
        {
            "createTime": "2020-10-07T00:04:41.669274Z",
            "expirationTime": "2021-04-08T00:00:00Z",
            "id": "212fd3eb-b919-4de5-8e21-7807b1997d18",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dcefe",
            "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
        }
    ]
}
```

We must now take the ID of the relevant ballot for the required combination of investor ID and poll ID, which in this case is `212fd3eb-b919-4de5-8e21-7807b1997d18` and use this ballot ID to call the `castVote` endpoint as shown

```shell
export INVESTOR_ID=d9d72655-ffca-4548-bac3-defd131dcefe
export BALLOT_ID=212fd3eb-b919-4de5-8e21-7807b1997d18

curl --location --request POST 'https://api.dev.tumelo.com/v1/habitats/'$HABITAT_ID'/investors/'$INVESTOR_ID'/ballots/'$BALLOT_ID'/castVote' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN \
--data-raw '{
    "response": "for"
}'
```

On successful submission of the vote preference, the response will be similar to the following, where the voting preference information that was submitted is now included.

```json
{
    "createTime": "2020-10-07T00:04:41.669274Z",
    "expirationTime": "2021-04-08T00:00:00Z",
    "id": "212fd3eb-b919-4de5-8e21-7807b1997d18",
    "investorId": "d9d72655-ffca-4548-bac3-defd131dcefe",
    "investorVote": {
        "response": "for",
        "responseTime": "2020-11-17T09:42:35.105455Z"
    },
    "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
}
```

Now that a vote preference has been received for investor `d9d72655-ffca-4548-bac3-defd131dcefe` for poll `0a0b3061-200d-4b1b-82da-034189614592`, that preference will be included in the results reported by Tumelo to the relevant fund managers. The investor should not be allowed to resubmit a vote preference for the same poll as this is not permitted, and the the `castVote` endpoint will return an error.