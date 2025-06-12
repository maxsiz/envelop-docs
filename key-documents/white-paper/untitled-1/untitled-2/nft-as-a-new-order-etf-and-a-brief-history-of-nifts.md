# NFT as a new order ETF and a brief history of NIFTSY

First, what is an ETF? An exchange-traded fund (ETF) is an index fund whose units (shares) are traded on an exchange. That is, it's almost a unit, but unlike an index mutual fund, ETF shares can be handled in the same way as ordinary shares in exchange-traded trading.

Why would a crypto market need this? There are several answers to the question:

* **First**, it's far more convenient for newcomers to take off-the-shelf portfolios (discussed below) than to build their own from scratch, especially if we don’t mean the top 10 currencies/tokens. Just look at the history of crypto market from 2009 (1 asset) till 2021 (more than 7000 assets, not including derivatives) to understand that such a model will be demanded.
* **Second**, for professional investors, portfolio sharing, diversification, objective asset valuation is important, and diversity is also confusing here. But most importantly, it does not always allow for a quick and accurate valuation of those assets. Another problem is that it makes difficult to exchange portfolios, to disclose them or, conversely, to remain anonymity. OTC transactions require a collateral guarantor, while an ETF created via NFT can be traded solely through Protocol.
* **Thirdly**, the evolution of P2P-systems is direct evidence of the Pareto rule’s work: 80% of the activity is created by 20% of the players. At least, initially. And here it is important to avoid manipulation: the Protocol provides this possibility exactly, and Oracle and the Index extend the functionality to a complete objective system of self-assessed assets.

The Protocol is the basis for next-order protocols. That is, while any blockchain solution is L0/L1 level, a protocol can lie in the L1/L2 plane and beyond. And NIFTSY offers the following in this vein:

* **First**, tokenization of payment channels. In this case, it doesn't matter whether we are looking at any specific implementations (Plasma, Lighting Network) or their aggregations (Plasma + ZK-rollups, bridges of different levels), whether we take a single blockchain or multi-chain integration. But the important thing is that the exit from the main chain can and should be used, providing liquidity to both the channel itself (between the parties) and the assets wrapped through the one (before closing the channel). In this case, the same mechanics of the cross-chain Protocol apply as when the Project links the offline economy with online projects.
* **Secondly**, the Protocol does not work by itself, but together, with other elements, serves as a decentralized on-chain cross market price discovery feature of any blockchain solution. That is, whether you make a secured fiat deposit and exchange it for an equal amount of tokens and/or coins of different order in the P2P economy, or exchange equivalent assets wrapped in NFT in different blockchains, the mechanics of the Protocol will be the same, and thus verifiable for each participant of the transaction.
* **Third**, the Protocol is a normalizer of relationships between different participants in DEX, DAO (DeFi) markets regardless of which SAO (subject-object) that participant is. For this reason, the Project can be integrated not only with classical P2P-markets, but also, for example, with IoT-solutions, where the main actors are programmable devices, hardware evaluation scripts or (semi) autonomous AI-systems that provide direct interaction between different IoT-elements.

Fourth, the Protocol actually creates the possibility of liquidity aggregation through cross-chain transfer of NFT ownership. B2Bx, 1inch and similar liquidity aggregators could be considered the closest analogue, but with the difference that they represent the first generation of this evolutionary branch of the DAO & DEX sphere.

However, the possibilities of the Protocol do not end there. Let's try to describe them very briefly, but in detail from a general development perspective.

On the one hand, the trend towards the integration of DeFi and NFT is clear today, because interchangeable tokens (ERC-20, TRC-20, BIP-20, etc.) can be exchanged at different levels: atomic swaps, if we are talking about blockchain solutions (DCR-LTC and others); via smart protocols like Bancor; directly via DEX & DAO solutions, the first and simplest implementation of which is DeFi. On the other hand, it is thanks to NFT wrappers that exchanges between different blockchain solutions (hereafter also referred to as DDS: decentralized and/or distributed systems) are possible without resorting to bridges or even more complex implementations. Above are examples of this aspect - Uniswap, YFI.Finance, AAVE.

But at the same time another important aspect arises - the problems of the NFT market itself. Here are just a few of these problems.

* **Firstly**, [the NFT market is too narrowly](https://blog.envelop.is/nfts-market-meta-analysis-by-niftsy-e9f131234041), not at the theoretical level where there were formats like ERC-721, ERC-998, ERC-1050 and many others that are constantly evolving, but precisely at the application level, as the NFT niches that became in demand between 2014 and 2021 were incredibly small: the gaming industry, digital art, off-line avatarization. But even these niches were able to contribute quite solid capitalization to the market both in terms of average check per NFT and maximum allowable parameters as well as project totals.
* **Second**, NFTs are in many ways vulnerable to attack not at the level of protocols and DDS in general, and at the level of the ultimate acquirer - the entity: starting with the fact that visible ID (identifier) substitution of an entity attached to an NFT is possible. And even if it also exists online (NFT phishing), not to mention complex off-line integrations, to the fact that it is quite difficult for a simple layman, just entering the industry, to determine the price of a non-fungible token.
* **Thirdly**, NFT also has other childhood diseases inherent to any innovation project in its infancy:
  * low network capacity;
  * shortage of liquidity in the markets;
  * others.

As Envelop's CTO correctly and accurately described, "I think the generic features of the protocol are:

1. **OnChain**. All events from the outside world are either cases of using the Protocol or an OTHER layer protocol built on top of our OnChain-Core;
2. Everything about NFT".

That means, everything that is done outside the Protocol (at a level below, above and/or several levels above) is either a new level protocol (L0, L2, L3), or oracles that somehow interact with them, or some kind of third entity.

That said, there are two main types of oracles:

* those that link the blockchain to the outside world: chain.link is an example of this;
* those that analyze the blockchain and produce a corpus of data on it, and already that data is used by other blockchain solutions, decentralized ones included: chainalytics.com.

In this case, we are talking about the first and second point at once, i.e. the third type of Oracle the synthetic one. On the one hand, it has to analyze all the data coming through the Protocol, and on the other hand it has to link the Protocol with the outside world.

That is why a study of this market and its segments was conducted in November-December 2020 (#01 and #02), and later - in the Spring of 2021 - the overall architecture of ENVELOP (NIFTSY) was developed, and then the was MVP presented at the Hackathon of the largest crypto exchange among others.

It is for this reason that, an answer to the question, "What problems does the Protocol solve?" was the team's joint response that the first and main problem being solved is securing NFT by putting various digital, and any tokenized NOT digital, assets inside a Container/Collateral (Collateral), or collateral drive in the future. This could be wrapped bitcoin (WBTC and others), ERC-20 and/or BIP-20 tokens, cryptocurrencies of various types, etc. The Protocol is initially built on the Ethereum blockchain (including via the L2 layer, for example, Polygon) and BSC, but in the future (see Roadmap) it is planned to create implementations on  WAX, Zilliqa, Near and other **DDN**, because we are deeply convinced cross-chain is the future of all decentralized and distributed systems. Exactly the same applies to second and subsequent layer solutions.

Let's summarize the conclusions about the Protocol which:

1. Allows the unification of **WUM**;&#x20;
2. Has a simple or multi-collateral;
3. Contains a static and a dynamic storage part;&#x20;
4. Serves as a zero-level evaluation of NFT of any order (as well as any derivatives) for the average user;
5. For B2B-players, it provides a mechanism for dealing with liquidity wrapped in NFT of any order on the one hand. On the other hand, the Protocol provides a clear mechanism for creating NFT (is a B2B -supplier of NFT);
6. Acts as an objective asset valuation tool where any fund client receives NFT unwrapped on an event/date and always knows exactly the primary collateral level of that NFT for funds (pension, insurance, investment, hedge, etc.).

But the Protocol cannot and shouldn’t have solved all the problems of the NFT market and its links with DeFi and other industries. This is how Oracle came about.
