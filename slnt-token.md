# SLNT Token

**Continuous Tokens** are a new kind of token managed by bonding curve contracts, named as such due to how its price is continuously calculated. A continuous token has interesting properties, such as:

* **Limitless supply.** There is no limit to the number of tokens that can be minted.
* **Deterministic price.** The buy and sell prices of tokens increase and decrease with the number of tokens minted.
* **Continuous price.** The price of a token `n` is less than a token `n+1` and more than token `n-1`.
* **Instant liquidity.** Tokens can be bought or sold instantaneously at any time, the bonding curve acting as an automated market maker. A bonding curve contract acts as the transaction's counterparty and always holds enough SLNT in reserve to buy tokens back.

### Bonding Curves

A **bonding curve** is a mathematical curve that defines a relationship between price and token supply. Here’s an example of a bonding curve, where `currentPrice = tokenSupply²`:

<figure><img src="https://cdn-images-1.medium.com/max/1600/1*rvTSneINGx3IunJcdjW8Ew.jpeg" alt=""><figcaption><p>bonding curve</p></figcaption></figure>

This bonding curve says that the price increases as the supply of the token increases. In the case of an exponential curve such as the one above, the growth rate accelerates as the number of tokens minted increases.

When a person has purchased the token, each subsequent buyer will have to pay a slightly higher price for each token, generating a potential profit for the earliest investors. As more people find out about the project and buying continues, the value of each token gradually increases along the bonding curve. Early investors who find promising projects early buy the curve-bonded token and then sell their token back can earn a profit in the future.

{% hint style="info" %}
You can have [different curve shapes](https://medium.com/thoughtchains/on-single-bonding-curves-for-continuous-token-models-a167f5ffef89) to accomplish different goals and properties.
{% endhint %}

### Mathematical Formula

The [Bancor](https://www.bancor.network/) Formula allows us to calculate the dynamically changing price of a Continuous Token. The formula relies on a _constant_ **Reserve Ratio** that is calculated as:

<figure><img src=".gitbook/assets/undefined - Imgur.png" alt=""><figcaption><p>Reserve Ratio</p></figcaption></figure>

{% hint style="info" %}
The Reserve Ratio is expressed as a percentage greater than 0% and up to 100%.
{% endhint %}

The Reserve Ratio represents a fixed ratio between the Continuous Token’s total value (total supply × unit price) and the value of its Reserve Token balance. This ratio will be held constant by the Bancor Formula as both the Reserve Token balance and the Continuous Token’s total value (a.k.a. ‘market cap’) fluctuate with buys and sells.

Since each purchase or sale of a Continuous Token triggers an increase or decrease of Reserve Tokens and Continuous Tokens, the price of the Continuous Token with respect to its Reserve Tokens will continuously recalculate to _maintain_ the configured reserve ratio between them.

### Reserve Ratio = Price Sensitivity

The Reserve Ratio determines how sharply a Continuous Token’s price needs to adjust in order to be maintained with every transaction, or in other words, its _price sensitivity_.

<figure><img src=".gitbook/assets/qYnG26I - Imgur.png" alt=""><figcaption><p>Price Sensitivity Graphs</p></figcaption></figure>

### Bonding curve price formulas

#### Simplifying the bonding curve price formulas

#### Basic Formulas

Let R be the current reserve of the parent currency (say, Ether). Let S be the current outstanding supply of tokens. Let F be the constant fractional reserve ratio, and finally, let P be the current price of a token. The total market cap of the tokens is SP, and by definition, the amount in reserve is F times that R = F SP. This means that the price at any time can be calculated as P = R SF. When a user buys an infinitesimal amount of SLNT dS (selling simply means dS < 0), the supply of tokens increases by this amount. The user pays P dS for them, which are added to the reserve, meaning dR = P dS. Additionally, since R = F SP, we have dR = d(F SP) = F d(SP) = F(S dP + P dS). So we have:

$$
P dS = dR = F(S dP + P dS)
$$

$$
P dS(1 − F) = F S dP
$$

<figure><img src=".gitbook/assets/Screenshot 2022-09-04 at 5.04.58 AM.png" alt=""><figcaption><p>Basic Bonding Curve Formula</p></figcaption></figure>

#### Continuous Token Price

<figure><img src=".gitbook/assets/undefined - Imgur (1).png" alt=""><figcaption><p>Continuous Token Price</p></figcaption></figure>

Recall that the price of a Continuous Token increase as the supply of continuous tokens increase. Buying slides you up the price curve and selling slides you back down. Calculating price thus becomes problematic when you want to exchange a plural amount of tokens.

Calculating the number of tokens minted for a given amount of SLNT (or the number of SLNT sent back for a given amount of tokens) requires **integral calculus** because we need to compute the area under the bonding curve:

<figure><img src="https://cdn-images-1.medium.com/max/1600/1*n8acuM7F7YmIKwZxpaZT4A.jpeg" alt=""><figcaption><p>Volume of SLNT minted</p></figcaption></figure>

From the original formula, two new formulas can be derived. One to calculate the number of continuous tokens one receives for a given number of reserve tokens:

$$
PurchaseReturn = ContinuousTokenSupply * ((1 + ReserveTokensReceived / ReserveTokenBalance) ^ (ReserveRatio) - 1)
$$

​And another to calculate the number of reserve tokens one receives in exchange for a given number of continuous tokens:

$$
SaleReturn = ReserveTokenBalance * (1 - (1 - ContinuousTokensReceived / ContinuousTokenSupply) ^ (1 / (ReserveRatio)))
$$

