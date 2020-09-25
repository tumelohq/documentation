# What is Shareholder Voting

Tumelo's mission is to enable retail investors and pension members to create and benefit from a more sustainable investment system.

We start by giving investors and pension members [transparency](../What_is_Transparency/README.md) over their investments, allowing them to see and learn about the companies they are invested in. Empowered with this knowledge, our shareholder voting system then gives investors and pension members a voice on issues they care about at those companies, such as gender equality, human rights or climate change.

## How it works
At least once a year every publicly listed company (e.g. Facebook, Google, Tesla) must hold an Annual General Meeting where questions related to corporate policy are asked for shareholders to vote on.

Shareholders can use their votes to persuade company management to take action on important issues like climate change and gender equality. This is one way for large asset owners and fund managers to influence key strategic decisions at the world’s biggest companies.

Tumelo's platform helps these large asset owners and fund managers understand what individual retail investors and pension members think about these issues ahead of time. Tumelo aggregates user views on upcoming shareholder questions such as:

* Should Microsoft report on the average gender pay gap?
* Should Alphabet build sustainability into executive pay?
* Should Walmart do more to stop sexual harassment?

We then feed user preferences back into the voting chain to inform stewardship teams.

Votes can cover a range of topics such as:

* Climate change
* Pay ratios
* Diversity
* Gender equality
* Human rights
* Recycling

We search for, research and write these votes based on available public information. We convert complex topics and language into a summary that our users can understand and use to place their own vote.

Tumelo's API allows third-party developers to seamlessly integrate investment transparency and shareholder voting functionality directly into their own digital product offerings, bringing these features directly to their own user communities.


## Data requirements
In order for an end-user investor to successfully vote we need:

* The ISINs of the instruments they hold
* The number of units they hold in each instrument
* The percentage weighting of each instrument by value relative to the overall account value

With this information the Tumelo transparency system is able to determine the full list of companies the user is invested in, either directly or indirectly through intermediate funds. For further details of how to use the Tumelo API to provide the data required to enable voting for an individual investor, please see the [Investor Account Transparency](../Investor_Account_Transparency/README.md) section.

**Important note:** Providing investor account holdings information is a prerequisite step for the subsequent use of the shareholder voting features described in this section. This is because we use the holdings of each individual investor to determine their eligibility to vote on any given AGM question. Voting features are only enabled for those investors for whom we have up to date holdings information.


## Proposals and Polls

The Tumelo API uses a number of different entities to provide shareholding voting. It is important to understand each of these entities, the information they contain, and the relationships between them in order to use the API effectively.

A **Proposal** entity represents the raw information about a single question being put forward at a given company AGM. An AGM proposal is sometimes referred to as an AGM *resolution*. The information in the proposal entity that's provided by the Tumelo API is taken directly from the publicly available official AGM documentation issued by the company. However, the majority of AGM proposals are written on the assumption that their primary target audience is the professional investor community. Often proposals contain jargon and terminology that is unfamiliar to most retail investors or pension scheme members, and they are not always easy to understand.

In order to make it easy for expert and non-expert investors alike to understand the question being voted on in a proposal, Tumelo's API provides the **Poll** entity. Tumelo's team of experts convert the complex topics and language of the raw proposal into a summary that is more easily understood. The poll entity contains this user-friendly version of a proposal. Every poll is linked back to its originating proposal so the full, original information is always available for the more curious investor should it be required. A poll is also related to the company whose AGM the poll is being voted on by their fund managers and the other company shareholders.


## Voting Eligibility and Ballots

For each poll, Tumelo uses current investor account transparency information to determine which investors are eligible to submit their voting preferences for that poll. Any investor holding a stake of any size in the poll's corresponding company is considered to be eligible to vote and they are issued a **Ballot**. The ballot is then used to submit the investor's voting preferences back to Tumelo. You can think of a ballot as being just like the ballot papers you receive at an election. As a voter, you mark your personal vote on the ballot paper and give it to the election operator, who then counts all the votes and reports the results to the relevant authorities.

A ballot entity, like voting papers, may only be used once. Once an investor's voting preference has been successfully submitted via the Tumelo API, the investor is no longer able to change their voting preference and is not able to vote again at the same poll.

Based on all the vote preferences submitted, Tumelo then informs the relevant fund managers of their member preferences in advance of the AGM itself.

In order to give fund managers time to consider member preference information in conjunction with all the other information they use to decide how they should vote in the best overall interests of their members, Tumelo needs to submit investor preference information in advance of the AGM date. For this reason polls have a closing time that's typically around 10 days before the AGM.

After a poll closes any unused ballots relating to that poll will expire and may no longer be used to submit an investor's voting preference.  If an attempt is made to submit a ballot after its expiry time, the API will return an error and the user voting preference will not be registered or included in any of the preference data that Tumelo passes to fund managers.

## Voting Outcomes
After an AGM has occurred and all the company's shareholders have cast their votes, the **Proposal** information is updated to add the details of the outcome of the vote at the AGM. This can be used to provide feedback to investors on how the majority of shareholders actually voted on the proposal at the AGM. The time that it takes for the AGM vote information to be made available to the public varies greatly. Sometimes it's available very quickly after the AGM, but in the worst case it can sometimes be several weeks later that the proposal outcome information is published and it becomes available through the Tumelo API.


## Further Factors Affecting Voting Eligibility
As described above, any time a new poll relating to a given company becomes available on the Tumelo system, any investor holding that company (based on the then current investor holdings data in Tumelo) is considered to be eligible to have their voice heard on that question, and the investor is automatically issued a ballot for the new poll.

Once a ballot is issued to an investor, they remain eligible to vote on the corresponding poll right up to the ballot's expiry time, regardless of how their holdings may change in the meantime. It does not matter if a subsequent update in their holdings information means that they no longer hold the relevant company. Having held the company at the time the poll became available is sufficient for the investor or pension member to have their voting preferences included in the investor preferences that are subsequently reported by Tumelo.

On the other hand, should an investor *not* hold a company at the time a new poll for that company becomes available, they will not be issued a ballot at that time. However, if a subsequent update to the investor's holdings means that they *do* now hold the company in question, then they will also be issued with a ballot to vote, so long as the poll is still open at the time of the holdings update.

In summary, so long as an investor has **any size of holding** in a company, at **any time** that a poll relating to that company is open, the investor will be eligible to vote, and will be issued with a ballot for the poll accordingly. For this reason it is important to keep investor holding information up to date with any significant changes.

## Privacy Policy

Tumelo never shares any personal or other identifying information relating to an investor with any third party. The investor preference data that we share with fund managers and other relevant organisations is always aggregated and totally anonymous. For full details of the information we collect about investors, how that information is used, and with whom it may be shared please see our [Privacy Policy](https://www.tumelo.com/privacy.pdf).



