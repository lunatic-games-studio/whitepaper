# Automated Market Makers(AMM)

In a typical cryptocurrency exchange (either centralized or decentralized), Market Makers create buy or sell orders for a particular token exchange pair, and Market Takers fill any satisfy participant orders to perform the exchange.

In this workflow, a matching process is necessary for an exchange to occur. Market makers need to create orders, orders need to be published on exchanges, market takers need to browse orders, and market makers need to wait for the orders to get filled. Because both buy and sell orders have prices attached to them, due to market fluctuations, there is the possibility that some orders may take a while to get filled, if ever.

{% hint style="info" %}
There must be a buyer and a seller available at the same time and in the same venue in order for the tokens to pass through the network. The challenge with consistently finding a match between buyers and sellers is a problem known in economics as the [double coincidence of wants](https://en.wikipedia.org/wiki/Coincidence\_of\_wants).

– [The Bancor whitepaper](https://storage.googleapis.com/website-bancor/2018/04/01ba8253-bancor\_protocol\_whitepaper\_en.pdf).
{% endhint %}

In contrast to traditional exchanges, Automated Market Makers (AMMs) use bonding curves to allow tokens to be seamlessly converted into one another in real-time without the need to match buyers and sellers. You can always buy and sell against the AMM contract.

## How Automated Market Makers Work

Each Automated Market Maker contract holds a balance of a Reserve Token (for example, a reserve balance of `ETH`). Buyers can use the reserve token to purchase a Continuous Token managed by the AMM (for example, a fictional token `PEPE`) by sending them to the Automated Market Maker contract, which adds the incoming amount to its reserve token balance and, in return, issues new Continuous Tokens, which are automatically sent back to the buyer.

The [Bancor Protocol](https://github.com/bancorprotocol/contracts-solidity) enables automatic price determination and an autonomous liquidity mechanism for tokens at a price that is continuously recalculated to balance buy and sell volumes. Prices are calculated using the Bancor formula:

$$
Continuous Token Price = Reserve Token Balance / (Continuous Token Supply x Reserve Ratio)
$$

Anyone can **always** purchase a Continuous Token by depositing some amount of its reserve token into its smart contract. In this case, both the reserve balance of the AMM has increased, as has the Continuous Token’s supply, since new units were issued. Similarly, a seller may send back any amount of Continuous Tokens to its contract, which will then remove these Continuous Tokens from circulation and withdraw a corresponding amount of Reserve Tokens from the AMM’s balance and send them to the seller. In this case, both the AMM’s Reserve Token balance and the Continuous Token’s supply have decreased.

## Summary

Automated market makers help bootstrap a liquid exchange from the very early days of a small-scale token communities. A common challenge in creating successful token-based communities is reaching a critical barrier where there are enough market participants to reach a liquid, healthy exchange of value. This is similar to the [chicken-and-egg problem](https://platformed.info/two-sided-market-seeding/) in market networks.

Users can always buy or sell tokens in the network directly through automated smart contracts, even when there are only few or no other buyers or sellers in the market.
