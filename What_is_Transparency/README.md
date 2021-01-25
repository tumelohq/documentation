# What is Transparency

Investment products such as pensions and stocks and shares ISAs can be quite complicated, and it is often difficult for an investor to get a clear picture of which companies their money is actually invested in. For example, a typical pension fund will include a large number of investments. Often those investments are themselves shares in other investment funds that are managed by specialist fund managers, for example with a particular interest in environment-friendly investments. These specialist funds may themselves include hundreds of individual investments, including holdings in other funds and so on. This is a normal investment practice and is done with the aim of achieving the goals of a specific investment product. 

If you dig down far enough through the layers of funds, ultimately the majority of equity-based investment products hold shares in individual companies that are listed on the global stock market. Sometimes they also hold some bonds and some cash too, depending on the fund.

**Transparency** at Tumelo provides users with the ability to understand the structure and contents of their accounts, funds or model portfolios. 

## Breakdown Types 

### Instrument Breakdown

Suppose we started with the above mentioned ISA account that contains funds. An instrument breakdown provides a view of that account in which the intermediary layers have been removed. Rather than providing the root view, the composition of the account, an organization breakdown is a view where constituent components are returned. Rather than returning the fund that is in the account, the view provided is one where we've gone to the funds underlying instrument constituents, for example, a share in a company and grouped the weighting of that share across all the account. If that share appears in more than one fund, the weight is aggregated to give an overall picture.

Sometimes it is not possible to fully attribute all the holdings of a fund to either to instruments or to cash. In this situation, the holding is included in the *others* category within the breakdown.

Instrument breakdowns may be used to investigate more granular exposure than the organization breakdowns mentioned below. Examples of use cases for instrument breakdowns are:

- Overall exposure to different asset classes
- Exposure to organizations by specific asset classes such as just the exposure to an organization through shares but not through bonds

### Organization breakdowns

Starting at a given investment fund, the Tumelo Transparency APIs make it easy to dig down through the layers of nested funds to get a consolidated list of all the companies that are represented within the top-level fund and to understand what proportion of the total fund value is invested in each of those companies. We refer to this as an **organization breakdown** of the investment fund. An organization breakdown essentially takes the instrument breakdown and maps all the known instruments to respective organizations. Equally, organization breakdown may include an organization such as HM Treasury who issue bonds. An organization breakdown result also identifies any known cash holdings in the fund. The organization breakdown provides a weight based view of a holding's exposure to a particular organization.

Most commonly the organizations listed are public companies whose shares are traded on the global stock markets, and the connection derived to the organization is equity based, i.e. the weight is attributed due to a share in that company. That said in an organization breakdown, **it can also be a bond or other instruments issued by the organization**.

Like instrument breakdowns, it is not possible to fully attribute all the holdings of a fund to either a company or to cash. In this situation, the holding is included in the *others* category within the breakdown.

By presenting an organisation breakdown to the end investor, they may have an easy way to understand view of which companies and other organizations their investments are exposed to. 

## Transparency of ...

The following outlines the different investment roots that Tumelo provides **Transparency** over. 

### A specific fund

The Tumelo API makes it easy to get the organization breakdown of any individual fund your company has subscribed to for the purposes of transparency. See the [Getting Started](../Getting_Started/README.md) guide for further information on *subscribed instruments*. If you require the organization breakdown of a fund your company is not already subscribed to, it is easy to add it by contacting [support@tumelo.com](mailto:support@tumelo.com).

For further details of how to obtain an organization breakdown on an investment fund using the Tumelo API, please see the [Instrument Transparency](../Instrument_Transparency/README.md) guide.

### An investor account

We have described how the Tumelo Platform API gives transparency to individual investment instruments, however, most investors have a pension or other investment product that contains many funds, and sometimes individual shares and cash as well. In order to make it easy to give a consolidated view of the companies held within an investor's account, see the [Investor Account Transparency](../Investor_Account_Transparency/README.md) guide.

### A model portfolio

In the situation where the same portfolio structure is shared by multiple investors, it is possible to set up one more model portfolios for your habitat. The Tumelo API supports providing transparency of a model portfolio through a model portfolio organization breakdown. See the [Model Portfolio Transparency](../Model_Portfolio_Transparency/README.md) guide for further details.
