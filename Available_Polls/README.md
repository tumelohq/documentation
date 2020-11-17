# Available Polls

## Overview

This guide explains how to discover which polls exist on the platform. For an overview of the poll entity, see the [What is Voting](../What_is_Voting/README.md) guide.


## Pre-requisites

* You must have signed up with Tumelo and obtained the credentials for your service user account (see [Getting Started](../Getting_Started/README.md) for further details)
* Your habitat must be subscribed to one or more composite instruments

## Polls

A poll represents an issue that has been voted on or will be voted on by the shareholders of a company at a shareholder meeting, typically the company's Annual General Meeting (AGM). As described in the [What is Voting](../What_is_Voting/README.md) guide, the poll for a specific issue generally closes in advance of the date of the AGM. This allows time for Tumelo to inform relevant fund managers of the voting preferences of their fund members.

## Listing polls that were open for voting within a date range
The [List Polls](https://docs.tumelo.com/#operation/listPollsInHabitat) endpoint provides a way of listing polls that are available on the Tumelo platform and _may_ be available (or may have been available) for one or more investors in your habitat to vote on. Individual investors will be issued ballots for all the polls they are actually entitled to vote on, as described in the [What is Voting](../What_is_Voting/README.md) guide. The `listPollsInHabitat` endpoint provides a convenient way of getting all the relevant information about a list of polls. Several optional filter parameters are supported, as described in the API reference.

For example the following request gets a list of the polls that were open for voting between midday on 1st Sept 2020 and midday on 10th September 2020:

```shell
curl --location --request GET 'https://api.prod.tumelo.com/v1/habitats/'$HABITAT_ID'/polls?closeTimeAfter=2020-09-01T12:00:00Z&closeTimeBefore=2020-09-10T12:00:00Z' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN
```

In the response, the outcome of the voting at the AGM will be included in the proposal `outcome` property if that information is available at the time the request is made. Additionally, the `tally` property gives the vote tally for investors within your habitat.

```json
{
    "polls": [
        {
            "closeAt": "2020-09-04T00:00:00Z",
            "formattedDescription": "### Background Info:\n\nThis time last year, Dixons Carphone (... additional content omitted ...). Although this vote is non-binding, we will use it to make future decisions on pay.",
            "id": "4cf1c987-be83-4a56-b3d0-39874297ab73",
            "publishAt": "2020-09-02T07:13:03.205587Z",
            "relationships": {
                "generalMeeting": {
                    "date": "2020-09-10",
                    "generalMeetingType": "annual",
                    "url": "https://www.dixonscarphone.com/sites/dixons-carphone-v2/files/dixon-v2/document/2020-notice-of-meeting-23-july-2020.pdf"
                },
                "organization": {
                    "bio": {
                        "description": "Dixons Carphone plc is a British multinational electrical and telecommunications retailer and services company headquartered in London, formed on 7 August 2014 by the merger of Dixons Retail and Carphone Warehouse Group. ",
                        "source": "wikipedia",
                        "sourceUrl": "https://en.wikipedia.org/wiki/Dixons_Carphone"
                    },
                    "displayName": "Dixons Carphone",
                    "externalIdentifiers": [
                        "LEI_2138001E12GWLLDQQF16"
                    ],
                    "id": "ec504914-0a3a-4276-9d60-53e7616f8432",
                    "legalName": "Dixons Carphone PLC",
                    "logoUrl": "https://res.cloudinary.com/tumelo/image/upload/w_128,h_128,c_fit/v1580303313/mzenfik6pb1u0glislrc.png",
                    "websiteUrl": "http://www.dixonscarphone.com/"
                },
                "proposal": {
                    "formattedDescription": "In accordance with the Act, (... additional content omitted ...)",
                    "id": "61003dce-b675-4a39-aced-1ae8cef71dd8",
                    "managementRecommendation": "for",
                    "outcome": {
                        "decision": "for",
                        "votes": {
                            "abstain": 0,
                            "against": 58771953,
                            "brokerNonVote": 2170977,
                            "for": 866889321
                        }
                    },
                    "passThreshold": 0.5,
                    "sequenceIdentifier": "2",
                    "source": "management",
                    "title": "Directors' Annual Remuneration Report"
                }
            },
            "tags": [
                {
                    "id": "2",
                    "title": "Equality"
                },
                {
                    "id": "9",
                    "title": "Management"
                }
            ],
            "tally": {
                "againstCount": 4815,
                "forCount": 2853,
                "validAt": "2020-11-17T13:17:10.526161267Z"
            },
            "title": "Do you approve of the CEO's pay at Dixons Carphone?"
        }
    ]
}
```

**Note:** _the information contained in the example above is for illustration purposes only. It should not be relied on as being accurate and should not be used for any purpose other than understanding how this API functions._

## Polls that are currently available to vote on
Similarly to the above example, by setting the `closeTimeAfter` query parameter to the current time, and omitting the `closeTimeBefore` parameter, you will get a list of all the polls that are currently open for voting. Any investor who has been issued with a ballot for one of those polls would be able to submit submit their vote preference using the `castVote` endpoint (see the [Casting a Vote](../Casting_a_Vote/README.md) guide), so long as they do so before the poll's close date and the ballot's expiry date (these are generally the same).

## Recently published polls
When a poll is made available to the platform, it is said to have been 'published'. The poll's `publishAt` property is the time the poll was first made available on the platform. The query parameter `publishedAfter` of the `listPollsInHabitat` endpoint can be used to list the polls that have recently been made available on the platform. This information can be valuable as part of a notification system that draws the availability of any new polls to the attention of investors, though only those investors who have actually been issued a ballot for a given poll will be able to vote on it.
