# Investor Ballots

## Overview

This guide explains how to discover which polls are available for an investor to vote on and which polls they have already voted on. The ballot entities associated with a given investor provide the information required. For an overview of the ballot and poll entities, see the [What is Voting](../What_is_Voting/README.md) guide.


## Pre-requisites

* You must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)
* Your habitat must be subscribed to one or more composite instruments
* You must have created one or more investors
* At least one investor must have an investor account with at least one composition record (see [Investor Account Transparency](../Investor_Account_Transparency/README.md)).

## Ballots

A ballot is issued to any investor that is entitled to submit their voting preference on an upcoming AGM proposal to the Tumelo platform. For details of how Tumelo determines whether an investor should be issued a ballot for a forthcoming vote, see [What is Voting](../What_is_Voting/README.md). Each ballot instance allows a specific investor to provide their voting preference on one specific issue.

An issued ballot may be used a maximum of once to register an investor's voting preference on a specific matter. Furthermore, every ballot has an expiry time before which the investor's preference must be registered in order for it to be counted and reported to the relevant fund manager(s).

## Listing Ballots For A Specific Investor

The [List investor ballots](https://docs.tumelo.com/#operation/listInvestorBallots) API endpoint may be used to retrieve a full list of all the ballots associated with a specific investor. The endpoint supports a range of optional query parameters that allow the returned list of ballots to be filtered according to a wide range of parameters. By suitably combining the optional query parameters, you can retrieve the set of ballots that are relevant to many different use cases:

* Ballots for which the investor hasn't submitted a vote preference yet (i.e. unused ballots).
* Ballots for which a user has already submitted their vote preference.
* Ballots that are closed and no longer available to submit vote preferences.
* Ballots for polls that are still open and accepting the submission of investor vote preferences.
* Ballots that have been newly issued since a specific date

This API endpoint may return a large number of ballots. In common with many Tumelo API endpoints, the results are paginated and multiple calls to the API may be required in order to retrieve the full set of results. Please see the [Pagination](https://docs.tumelo.com/#section/Using-the-API/Pagination) section in the API reference guide for further details.

### Ballots available for submitting a vote preference 
The following example request would return all ballots for a given investor that had not expired as at 10pm on 24th October 2020 and had not yet been used to submit a vote preference.

```shell
export INVESTOR_ID=d9d72655-ffca-4548-bac3-defd131dceff

curl --location --request GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/investors/'$INVESTOR_ID'/ballots?expireAfter=2020-10-24T22:00:00Z&hasVoted=false' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN \
```

This request will return a response similar to the following

```json
{
    "ballots": [
        {
            "createTime": "2020-10-07T00:04:41.669274Z",
            "expirationTime": "2020-11-07T00:00:00Z",
            "id": "212fd3eb-b919-4de5-8e21-7807b1997d18",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dceff",
            "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
        },
        {
            "createTime": "2020-10-23T00:06:25.017864Z",
            "expirationTime": "2020-11-18T00:00:00Z",
            "id": "d248447c-7397-467a-a005-447b55535792",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dceff",
            "pollId": "49869f93-c852-405a-b001-545e5f0a310c"
        },
        {
            "createTime": "2020-10-23T00:06:25.037532Z",
            "expirationTime": "2020-12-01T00:00:00Z",
            "id": "d8617628-9b93-4aee-9395-5d2b753fba56",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dceff",
            "pollId": "6f566ee3-2365-4d6d-ba99-eb02e86c9377"
        }
    ]
}
```

### Ballots already used to cast a vote
The following request would return a list of all the ballots that have already been used to submit a vote preference by the given investor since they were registered with Tumelo. Note that subsequent requests may be required to retrieve the complete paginated response.

```shell
export INVESTOR_ID=d9d72655-ffca-4548-bac3-defd131dceff

curl --location --request GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/investors/'$INVESTOR_ID'/ballots?hasVoted=true' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN \
```

This request will return a response similar to the following, where the ballots returned now also include the information on how the investor voted and the time the investor's vote preference was submitted.

```json
{
    "ballots": [
        {
            "createTime": "2020-10-07T00:04:41.682436Z",
            "expirationTime": "2020-11-30T22:00:00Z",
            "id": "195556ef-6830-43d1-bb12-c3e384768413",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dceff",
            "investorVote": {
                "response": "for",
                "responseTime": "2020-11-10T16:03:03.07952Z"
            },
            "pollId": "26776e6e-453d-4672-a878-abbcd5226e56"
        }
    ]
}
```

## Listing All Ballots

In some situations it may be desirable to retrieve ballots for _any_ investor within your habitat according to specific criteria. For example you may want to retrieve a list of all the ballots that have been newly issued to any of your investors within in the last day so that you could notify them of the new opportunity to vote.

This can be achieved with an Investor ID wildcard, using the same [List investor ballots](https://docs.tumelo.com/#operation/listInvestorBallots) endpoint as above. Rather than specifying the investor's UUID as a path parameter, you should use the `-` wildcard character. The optional query parameters work in exactly the same way as above.

For example, the following request would return ballots for all investors in the habitat that were created after 22:00 on 22nd October 2020 that didn't expire for at least 48 hours after they were created and that had not yet been used to submit a vote preference.

```shell
curl --location --request GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/investors/-/ballots?createdAfter=2020-10-22T22:00:00Z&expireAfter=2020-10-24T22:00:00Z&hasVoted=false' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN \
```

The above request will return a response similar to the following

```json
{
    "ballots": [
        {
            "createTime": "2020-10-07T00:04:41.669274Z",
            "expirationTime": "2020-11-07T00:00:00Z",
            "id": "212fd3eb-b919-4de5-8e21-7807b1997d18",
            "investorId": "d9d72655-ffca-4548-bac3-defd131dceff",
            "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
        },
        {
            "createTime": "2020-10-07T00:04:41.669274Z",
            "expirationTime": "2020-11-07T00:00:00Z",
            "id": "7535882d-247f-4b9d-a3e9-54b8ee87b8b0",
            "investorId": "618297cc-cec9-471c-b895-07cf68f7b1c0",
            "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
        },
        {
            "createTime": "2020-10-07T00:04:41.669274Z",
            "expirationTime": "2020-11-07T00:00:00Z",
            "id": "62d123e7-32a8-48bd-b012-62e0b3f0d954",
            "investorId": "6b503f61-6395-4d7d-97f2-fa73e32e7b74",
            "pollId": "0a0b3061-200d-4b1b-82da-034189614592"
        }
        ...
    ]
}
```


