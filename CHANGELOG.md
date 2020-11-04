# CHANGELOG

| Version | Date | Changes |
|-|-|-|
| 0.45 | 4 Nov 2020 | Updated error cases for listBallots endpoint. |
| 0.44 | 3 Nov 2020 | Added filters to listBallots endpoint. |
| 0.41 | 22 Oct 2020 | Added pagination to listBallots endpoint. |
| 0.40 | 22 Oct 2020 | Breaking: Added pagination to listPolls endpoint. |
| 0.38 | 20 Oct 2020 | Breaking: Allowed listing all investors and added pagination to listInvestors endpoint. |
| 0.36 | 13 Oct 2020 | Added `validAt` time to the poll Tally. |
| 0.35 | 9 Oct 2020 | Added tally to poll entity. |
| 0.34 | 15 Sept 2020 | Added authenticate and changePassword endpoints. |
| 0.33 | 2 Sept 2020 | Added list ballots endpoint. |
| 0.32 | 24 July 2020 | Breaking: Removes the subscribed instruments endpoint replacing it with a new `/habitats/{habitatId}/instruments` endpoint. The new endpoint returns a list of instrument resources the habitat is subscribed to, rather than just the list of subscribed ISINs. |
| 0.31 | 22 July 2020 | Reword compositions and breakdowns section. |
| 0.30 | 17 July 2020 | Update investor account organization breakdown request error description. |
| 0.29 | 17 July 2020 | Update investor account organization breakdown request title. |
| 0.28 | 17 July 2020 | Breaking: Remove global instrument breakdown endpoint. |
| 0.27 | 17 July 2020 | Change tags for organization breakdown endpoint. |
| 0.26 | 17 July 2020 | Add ability to get organization breakdown on an account. |
| 0.25 | 16 July 2020 | Breaking: Remove the global organization breakdown endpoint. |
| 0.24 | 16 July 2020 | Breaking: Rename validAt and createdAt to validTime and createTime in Investor Account Composition requests. |
| 0.23 | 14 July 2020 | New Feature: Add the organization breakdown endpoint under a specific habitat. |
| 0.22 | 8 July 2020 | Change definition of `ids` list parameter in listOrganizations. |
| 0.21 | 8 July 2020 | Remove deprecated proposal `proposalDescription` property. |
| 0.20 | 8 July 2020 | Add `externalIdentifiers` field to listOrganizations endpoint. |
| 0.19 | 8 July 2020 | Remove organization `identifiers` property. |
| 0.18 | 8 July 2020 | Add formattedDescription to proposal and deprecates proposalDescription. |
| 0.17 | 7 July 2020 | New Feature: Add investor account compositions. |
| 0.16 | 6 July 2020 | Breaking: Change behaviour of GetOrganization to use internal uuid rather than external IDs. |
| 0.15 | 6 July 2020 | Deprecation: Deprecate organization `identifiers` field, Add organization `externalIdentifiers` field. |
| 0.14 | 24 June 2020 | New Feature: Add ability to fetch subscribed instruments. |
| 0.13 | 18 June 2020 | New Feature: Add investor accounts. |
| 0.12 | 15 June 2020 | Breaking: Refactor Breakdown types, remove unused ISIN in InstrumentBreakdown, make basedOn all non-required and consistent. |
| 0.11 | 12 June 2020 | Breaking: Remove Get Poll endpoint. |
| 0.10 | 03 June 2020 | New Feature: Add proposal outcome to the proposal in poll relationships. |
| 0.9 | 12 May 2020 | Breaking: Update organization to make legalName required instead of displayName. |
| 0.8 | 02 April 2020 | Breaking: Update organization breakdown `basedOn` property to allow the inclusion of both `instruments` and `modelPortfolios`.<br>New Feature: Add modelPortfolios and polls.|
| 0.7 | 11 March 2020 | New Feature: Add investor functionality. |
| 0.6 | 09 March 2020 | Breaking: Rename schema properties: `logoURL`, `sourceURL` and `websiteURL` to `logoUrl`, `sourceUrl` and `websiteUrl` respectively. |
| 0.5 | 04 March 2020 | Breaking: Remove `code` from error object. Remove `isin` from breakdown. |
| 0.4 | 12 February 2020 | Breaking: Change organization breakdown to return organization summary rather than just identifiers. |
| 0.3 | 11 February 2020 | Breaking: Change the organization bio from a string to an object with source. |
